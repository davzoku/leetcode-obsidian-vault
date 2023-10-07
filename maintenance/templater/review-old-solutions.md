<%*
/* === Installation ===
 * https://gist.github.com/dsteinbock/d61bd359f85a5ade4a46834f1b290719
 * 1. Make sure you have both Templater and Dataview installed.
 * 2. Create a new template note.
 * 3. Copy and paste the full code from this file you're reading.
 * 4. Launch the script by using the Templater command "Open Insert Template modal".
 * 5. Optional, assign this script to a hotkey using the Templater settings page.
 *
 * v1.0.3
 */

// === Configuration settings ===

// The frontmatter field you want to store the last reviewed date
const YAML_FIELD = 'last_reviewed'

// How many results to return from the search
const NUMBER_OF_RESULTS = 5

// Only show notes that were last reviewed at least this many weeks ago
const ONLY_NOTES_OLDER_THAN_X_WEEKS = 4

// Weight older results. A value of 5 means the oldest note is 5x more likely to appear than the newest note
const WEIGHT_OLDER_NOTES = 5

// Select notes only from these folders (and subfolders).
// [] is all notes from all folders
// ['Journal','Daily/2022'] is the notes from Journal and Daily/2022 folders and subfolders
// You can also use a string in Dataview's `sources` format for a more advanced query:
// https://blacksmithgu.github.io/obsidian-dataview/query/sources/
const FOLDERS = []

// Personally I want to review my unfiled Inbox notes as the highest priority.
// If you want that functionality, set your Inbox folder path here, and if there
// are any unprocessed notes, the script will simply open the first unprocessed note.
const INBOX = 'undefined'

// Set to true if you want notes with no inlinks or outlinks to be displayed as priority before unreviewed notes.
const ORPHAN_NOTES = false

// Custom age display (highly abbreviated, in this case)
moment.updateLocale('en', {
    relativeTime : {
        future: "in %s",
        past:   "%s ago",
        s  : '%ds',
        ss : '%ds',
        m:  "%dm",
        mm: "%dm",
        h:  "%dh",
        hh: "%dh",
        d:  "%dd",
        dd: "%dd",
        w:  "%dw",
        ww: "%dw",
        M:  "%dM",
        MM: "%dM",
        y:  "%dy",
        yy: "%dy"
    }
});
// === End of configuration settings ===

const dv = app.plugins.plugins.dataview.api

let pages = []
// Get inbox notes first if configured
if (INBOX) {
    pages = dv.pages('"' + INBOX + '"')
    if (pages.length) new Notice('Found Inbox note to process', 5000)
}
// Get orphan notes if configured
if (ORPHAN_NOTES && !pages.length) {
    pages = dv.pages(FOLDERS).where(x => !x.file.inlinks.length && !x.file.outlinks.length)
    if (pages.length) new Notice('Found note which needs inlinks or outlinks', 5000)
}
if (pages.length) {
    // Open the first note for review
    const file = app.vault.getAbstractFileByPath(pages[0].file.path)
    await app.workspace.getLeaf(false).openFile(file)
    return ''
}

// Turn folders config option into Dataview search format
let location
if (Array.isArray(FOLDERS) && FOLDERS.length) {
    // Array location format
    location = '"' + FOLDERS.join('" or "') + '"'
} else if (typeof FOLDERS === 'string') {
    // Dataview sources format
    location = FOLDERS
}

/**
 * Get the last reviewed time of the page as milliseconds-since-epoch.
 * If there is a YAML field available it will return that,
 * otherwise will return the page last-modified date.
 * 
 * @param {Object} page - A Dataview page object
 * @returns {number} Milliseconds since epoch
 */
function lastReviewed(page) {
    const frontmatter = page[YAML_FIELD] || page.modified // in case of a frontmatter 'modified' field
    return (frontmatter ? frontmatter.ts || moment(frontmatter).valueOf() : null) || page.file.mtime.ts
}

// Use Dataview to find all notes that match our age criteria
const time = moment().subtract(ONLY_NOTES_OLDER_THAN_X_WEEKS, 'weeks').valueOf()
pages = dv.pages(location).where(page => lastReviewed(page) < time).array()

if (!pages.length) {
    // Nothing to process
    new Notice('Nothing found to review', 5000)
    return ''
} else if (pages.length > NUMBER_OF_RESULTS) {
    // Select a list of random pages to present for review, with optional weighting
    pages.sort((a, b) => lastReviewed(b) - lastReviewed(a))
    // Select a random array of pages, weighting towards older results
    const exp = Math.log(pages.length * WEIGHT_OLDER_NOTES) / Math.log(pages.length)
    const randomResult = []
    let count = 0 // for safety, in case of an unknown overflow
    while (randomResult.length < NUMBER_OF_RESULTS && count < 1000) {
        const i = Math.floor(Math.pow(Math.random() * pages.length * WEIGHT_OLDER_NOTES, 1 / exp))
        if (!randomResult.includes(i) && pages[i]) randomResult.push(i)
        count++
    }
    pages = randomResult.map(i => pages[i])
} else {
    // Not enough pages to need weighting, so just randomly sort
    pages.sort(() => Math.random() - 0.5)
}

// Generate the text display values for the Suggester box
// Formatted to show time since last review, note name, note path
const textValues = Object.values(pages).map(page => moment(lastReviewed(page)).fromNow(true) + '\t    ' + page.file.name + '\n\t    ' + page.file.folder)

// Present the list of pages to choose from
const index = await tp.system.suggester(textValues, Object.keys(pages))
if (index === null) {
    return '' // No file chosen
}

// Update the reviewed status in the frontmatter 
const page = pages[index]
const file = app.vault.getAbstractFileByPath(page.file.path)
const fieldData = YAML_FIELD + ': ' + moment().format()
let contents = await app.vault.read(file)
if (page[YAML_FIELD]) {
    // This page already has the necessary frontmatter field, so just update it
    contents = contents.replace(new RegExp(`^${YAML_FIELD}:.*$`, 'm'), fieldData)
}
else {
    // Check for existing frontmatter section
    const cache = app.metadataCache.getFileCache(file)
    if (cache.frontmatter) {
        // Add the missing field to the end of the existing frontmatter section
        contents = contents.replace(/^---(.*?)---/s, '---$1' + fieldData + '\n---')
    } else {
        // Add a new frontmatter section to the page
        contents = `---\n${fieldData}\n---\n` + contents
    }
}
app.vault.modify(file, contents)

// Open the file for review
await app.workspace.getLeaf(false).openFile(file)
%>