---
title: "<i>Remove notes to avoid MAX_ITEMS error</i> pull request to fix Netflix Notes Chrome extension"
author: Daniel Dantas
# redirect: https://github.com/mmorearty/netflix-notes/pull/1
---

## [💻GitHub PR](https://github.com/mmorearty/netflix-notes/pull/1)

> The maximum amount of items an extension can place into [Chrome sync storage](https://developer.chrome.com/docs/extensions/reference/api/storage#property-sync) is [512 items](https://developer.chrome.com/docs/extensions/reference/api/storage#properties_4)--attempting to add any further items will result in a MAX_ITEMS error. As a result, when you've used Netflix Notes for some time and entered small notes for 512 films at various times over the years, attempting to add any further notes will fail with a MAX_ITEMS error, and the extension becomes unusable. The only fix I've determined is to uninstall and reinstall the extension, which loses all existing notes.

> With this change, if you are editing an existing note and you remove all text, the note for the film is removed from storage. The original version would update the existing note to be "add note" instead of removing the existing note. With the ability to remove existing notes, you can keep your note count well under 512.
