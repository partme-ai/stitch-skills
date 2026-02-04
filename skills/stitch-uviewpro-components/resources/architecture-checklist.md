# Architecture Quality Gate (uni-app + uView Pro)

## Structural integrity
- [ ] Pages under `pages/`; shared components under `components/`.
- [ ] Logic in script setup or composables; no monolithic single page.
- [ ] Static text, image URLs, lists in data or `data/mockData.js`.

## uView Pro usage
- [ ] Layout: Use `<u-row>`, `<u-col>`, `<u-gap>`, `<u-divider>`; rpx for typography/spacing.
- [ ] Buttons: Use `<u-button type="primary">` etc.; no raw `<button>`.
- [ ] Forms: Use `<u-form>`, `<u-form-item>`, `<u-input>`; labels present.
- [ ] Navigation: Use `<u-navbar>`, `<u-tabs>` per contract.
- [ ] List/feedback: Use `<u-swipe-action>`, `<u-list>`, `<u-toast>`, `uni.$u` per contract.

## Styling and tokens
- [ ] Use uView Pro design tokens (primary, main text, etc.); rpx for sizes.
- [ ] Scoped styles; avoid hardcoded hex when token exists.

## Quality
- [ ] Pages registered in `pages.json`; no placeholder "StitchPage" left.
- [ ] Run in HBuilderX or CLI; verify layout on simulator/device; script setup (Vue 3) used.
