1. PDF generator API (5 pts)
* new endpoint in our service
* pass payload → downstream PDF service
* return file with correct headers
* handle errors + logging
* no FE changes needed

2. Accounts API (3 pts)
* expose endpoint in our exp service
* call downstream service (no FE → external service directly)
* response matches current FE contract
* basic error handling + logging
* FE works without changes

3. Accessibility (3 pts)
* keyboard nav works
* add missing labels / ARIA
* fix contrast issues
* no major a11y violations

4. UI polish + tech debt (5 pts)
* remove hardcoded values → config/theme
* align spacing/fonts/etc with figma
* clean up components
* fix any minor UI defects
