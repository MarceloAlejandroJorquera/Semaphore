# Semaphore v1.1.1.1 — Exhaustive changes since v1.1.1

This changelog is intentionally exhaustive for the v1.1.1 → v1.1.1.1 development cycle.

## Added

- Protocol-selection modal live search embedded directly in the **Proto** header.
- Protocol search supports case-insensitive plain-text matching, `*` / `?` wildcards, and `/regular-expression/` matching.
- Live protocol result filtering while preserving the user's checked protocol selections.
- Dynamic protocol-modal height: one through seven visible result rows, with native scrolling above seven matches.
- Single merged **No results** row when a protocol search has no matches.
- Per-token ID Filter badges in the `+` manual policy-rule popup, matching the **Rules** visual model.
- Split D&T presentation into separate **date** and **time** badges in Outbound, Inbound, Through, and traffic-iteration detail tables.
- Traffic-history format v12 for the corrected Through iteration-detail schema.
- Backward-compatible restoration of v8-v11 Through iteration history into the new seven-column popup.

- ID and Protocol badges in Outbound/Inbound traffic-iteration modals, plus Protocol badges in Through iteration modals.
- Cross-store policy subsumption between legacy/imported address ranges and equivalent standalone Any/Any policy rows.
- Stable custom Protocol-search header strip that is independent of `QHeaderView` repaint/recycling.
- Badge-geometry-aware traffic column sizing for compact D&T/Protocol presentation.
- In-field Protocol selector filter glyph with three live modes: all protocols, checked protocols only, and unchecked protocols only.
- Blocked-country count in the Country policy tab label, matching the Blacklist/Whitelist count presentation.
- Alpha-fade edge treatment for long editable text fields, revealing hidden/truncated text boundaries without hard clipping.

## Changed

- Development/public version identity advanced from `v1.1.1` to `v1.1.1.1`.
- Qt application version advanced from `1.1.1` to `1.1.1.1`.
- Portable production executable is now emitted as `Semaphore-v1.1.1.1-win-x64.exe`.
- Portable archive name is now `Semaphore-v1.1.1.1-win-x64.zip`.
- Portable runtime payload version advanced to `1.1.1.1`.
- `Semaphore Test.lnk` now targets the versioned v1.1.1.1 portable executable.
- Main-window minimum geometry was iterated during development and finalized at **1366 × 520 px**, with the same minimum enforced through Qt sizing, native `WM_GETMINMAXINFO`, startup placement and tray restore.
- Manual `+` policy-rule popup no longer contains **Add** or **Exit** buttons; field values commit on normal editor commit/focus changes and the popup dismisses using normal popup behavior.
- Manual policy editor column widths are derived from header/content requirements to prevent header and cell clipping.
- Manual ID Filter display now uses content-sized badges rather than a comma-joined plain-text button.
- Through D&T and Protocol badge typography reduced by one additional step versus the v1.1.1 stable baseline.
- Through D&T width adjusted for the new two-badge date/time presentation; Through Protocol width tightened for the smaller badge typography.
- Outbound/Inbound D&T widths adjusted for the new two-badge date/time presentation.
- Through traffic-iteration modal order is `# | D&T | From | Port | To | Port | Proto`, matching the final live-table terminology.
- Release checker identifies the running build as `v1.1.1.1`; its GitHub API User-Agent now derives from the canonical version constant, while the existing variable-depth numeric comparator is retained because it already correctly handles the zero-free hierarchy (`v1.1.1.1`, `v1.1.1.2`, …, `v1.1.2`).

- Protocol search occupies the visible `Proto` header strip; the embedded input uses `Proto` as its placeholder and the same header typography.
- Protocol-search popup width/position stays stable while filtering; only the row-driven height changes.
- Manual `+` policy editor uses larger content-derived widths and falls back to a horizontal scrollbar only when the complete editor cannot fit on the available screen.
- ID Filter badge buttons use the inherited policy-table font and keep the cell background stable on hover, matching the Lists / policy presentation more closely.
- Through D&T and Protocol badge typography reduced by one further point; both column widths are now calculated from the reduced badge font and representative content rather than hard-coded widths.
- Through D&T/Protocol restored-history sizing now uses the same natural badge geometry as the delegate and may shrink as well as grow, eliminating trailing blank cell space.
- Manual-policy ID Filter editor paints badges directly on the table cell instead of adding a second inner input frame.
- Address-only policy stores are re-canonicalized during Lists refresh so exact duplicate ranges and equivalent cross-store Any/Any rules cannot survive merely because they came from older persisted state.
- Traffic selector cells with missing/legacy policy snapshots now resolve against the current canonical policy; genuinely untouched selectors render allowed/green instead of neutral gray.
- Protocol selector filtering combines the text/regex query with the new all/checked/unchecked state filter, and filtered rows update immediately when their checkbox state changes.
- Protocol filter-state glyph geometry is inset from the search field frame and uses DPI-safe internal padding so All/Checked/Unchecked icons remain fully visible.
- Clearing the final Port badge now explicitly resets the Port selector to `Any`; dismissing an untouched empty Port popup still cancels without creating a rule.
- Informational/help tooltips now use one application-wide Semaphore `QToolTip` treatment matching the Protocol filter control: dark surface, rounded corners and red underline; the yellow custom tooltip remains reserved for genuinely truncated table-cell full-value previews.
- Long QLineEdit values now fade at the actually hidden left/right edge(s), following the editor's horizontal scroll/caret position rather than ending in an abrupt hard clip.

## Fixed

- Truncated/touching headers and clipped editor geometry in the `+` manual policy-rule popup.
- ID Filter values in the manual-rule popup appearing as one plain comma-separated string rather than individual badges.
- Manual-rule popup requiring explicit Add/Exit controls despite popup/editor commit behavior.
- Protocol selector always occupying seven visible rows even when a search has fewer matches.
- Missing live protocol filtering and missing explicit empty-search result state.
- D&T being rendered as one large badge instead of separate date/time badges.
- Through D&T / Protocol badge text sitting too close to the badge contour.
- Incorrect Through iteration-modal field order (`#`, D&T, Port, Origin, Port, Destination).
- Missing Protocol column in the Through iteration modal.
- Potential reinterpretation of v1.1.1 Through history after changing the detail-column mapping; v12 now preserves the legacy v11 six-field mapping during migration.
- Manual policy popup being considered modified merely because a pre-filled text editor lost focus; only actual text edits now mark the draft dirty.

- Protocol-search popup red-frame/header artifacts caused by re-centering and resizing the `Qt::Popup` on every keystroke.
- Protocol search input overlapping the header underline and leaving broken border fragments after result-count changes.
- Missing ID/Protocol badge rendering inside traffic-iteration modals.
- Manual policy editor default IPv4 range values and other contents appearing clipped inside fixed-width columns.
- Redundant rules remaining visible when a broader same-action Any/Any rule already completely subsumed narrower ID Filter or legacy/imported address-range rules.
- Potential quadratic range removal when a broad standalone rule subsumes a very large imported range set; reconciliation now filters ranges in a linear materialization pass.
- Protocol modal outer-frame corruption caused by placing the search editor inside `QHeaderView::viewport()`; the search field now lives in a fixed custom header strip with a permanent scrollbar gutter.
- Protocol modal child surfaces covering portions of the red popup frame during live filtering/resizing.
- Through D&T and Protocol columns retaining widths derived from raw 17 pt cell text even though the delegate paints smaller badges.
- Duplicate full-range address-only rows remaining visible after older state/migration paths bypassed normal range optimization.
- Extra inner rectangle around the manual `+` policy modal ID Filter cell.
- D&T and Protocol tooltips appearing in the Through table even when the visible badges were not truncated; tooltip detection now mirrors the actual badge font, split D&T tokens, spacing, padding and elision geometry.
- Legacy/restored Port, Flag, ID and Protocol cells appearing gray despite having no matching rule, by resolving unknown selector snapshots instead of treating every missing snapshot as neutral.
- Protocol state-filter checkbox/dash glyph clipping against the search-field right edge at fractional Windows DPI scaling.
- Deleting the last Port value from an existing rule restoring that deleted value because an empty Port popup was treated as cancel; explicit clearing now commits `Any`.
- Country tab omitting the number of currently blocked countries while Blacklist and Whitelist already exposed their counts.
- Protocol all/checked/unchecked filter-state glyph remaining undersized and visually clipped inside the search field; its child surface, checkbox outline and check mark now stay fully inside the editor at common Windows DPI scales.
- Inconsistent informational tooltip appearances across buttons, tabs, policy cells and helper controls by applying the same rounded/red-underlined style globally to standard QToolTip windows.
- Abrupt hard clipping of long text in Protocol search, Port, ID Filter, manual policy ID/range editors and inline policy ID editing by adding MJTC-style edge fading.

## Preserved

- v1.1.1 stable WFP policy/enforcement behavior unless explicitly changed above.
- Existing zero-free, variable-depth release-version comparison semantics.
- Existing multi-value ID Filter wildcard semantics and OR behavior.
- Existing protocol selections while protocol search results are filtered.
- Existing maximum of seven visible rows in protocol-selection popups.
- Existing historical traffic compatibility for earlier stored iterator formats.

## Empty-cell presentation

- Replaced the single diagonal empty-cell marker with a dense vertical parallel-line hatch.
- The hatch uses crisp 1 px lines with 1 px spacing across the cell, matching the requested presentation.
- Applied everywhere the previous diagonal marker was used, including empty traffic cells, missing flags, and disabled/empty Protocol/Port policy cells.
- Empty ID Filter cells remain intentionally blank and are not hatched.

### Header / tooltip typography regression

- Restored Semaphore's canonical **Anonymous Pro, bold, 17 pt** typography for table/header views after the application-wide informational-tooltip styling introduced an unintended native/default-font fallback.
- Informational tooltips now explicitly use the same canonical Semaphore font family, weight and size while retaining the new dark rounded style and red underline.
- Added a direct `QToolTip::setFont()` guard plus explicit header-font restoration for already-created views so Windows/Qt style-sheet fallback cannot silently revert them to the platform's small Arial/default UI font.
- The custom yellow truncated-cell tooltip remains unchanged.


### Input edge fade completion fix

- Corrected the MJTC-style QLineEdit edge fade so clipped glyph fragments can no longer remain visible at the left or right boundary.
- Added a fully opaque edge cap before the alpha falloff, rather than stopping at a high-but-translucent alpha value.
- Extended the cover slightly into line-edit padding to hide anti-aliased character remnants at the clipping boundary.
- Increased the fade span while keeping the transition gradual toward the visible text.
- The fade now samples the active style option's Base color first so focused/QSS-styled inputs retain the correct background while their clipped text is masked.
- Protocol's embedded filter-state control remains above the text fade and is not obscured.

### Input edge fade boundary hardening

- Reworked long-input edge fading to mask from the actual styled `QLineEdit` contents rectangle rather than the estimated text rectangle.
- Added an explicit fully opaque edge guard before each alpha ramp so fractional-DPI antialiasing cannot leave a one-pixel glyph fragment visible at the clipped boundary.
- Expanded the fade span slightly and paints across the complete usable input height, fixing the remaining left/right edge artifacts visible with long Protocol and policy input values.
- Preserved the soft alpha transition farther inside the field and preserved the Protocol state-filter glyph above the parent edit paint layer.

### Tooltip underline and minimum-width consistency

- Increased the application-wide informational `QToolTip` red bottom underline from 2 px to 3 px so ordinary tooltips match the stronger Protocol-filter tooltip presentation.
- Kept the yellow full-value tooltip used for genuinely truncated table cells unchanged.
- Top-level layout size-hint constraints no longer inflate the explicit main-window minimum; the final v1.1.1.1 minimum is `setMinimumSize(999, 520)`.
- Main content/tab layouts can now compress horizontally and rely on their existing table scrolling instead of preventing the native window from reaching the configured minimum width.
- Preserved the Windows native `WM_GETMINMAXINFO` minimum-track path so resize/Snap behavior continues to honor the explicit application minimum.



### Policy tooltip, badge, lane-font, input-fade and minimum-width refinement

- Raised the final v1.1.1.1 main-window minimum width from the temporary 666 px development value to **999 px** while preserving the 520 px minimum height and native `WM_GETMINMAXINFO` enforcement.
- Removed the former composite policy-ID tooltip that accumulated rule history/provenance and could continue showing previous IDs after an ID was renamed.
- ID cells now use only Semaphore's yellow full-value tooltip, only when the visible ID text is genuinely truncated, and the tooltip contains only that cell's current text.
- Blacklist/Whitelist First/Last IP cells now use the same yellow full-value preview only when their address text is actually truncated; untruncated addresses have no address-cell tooltip.
- ID Filter cells now use only the yellow full-value preview when their actual badge layout is clipped; empty or fully visible ID Filter cells have no tooltip.
- Lane, Proto and Port help text moved from individual policy cells to their respective table headers.
- Cleared stale `Qt::ToolTipRole` data from reused policy-table items so older composite/help tooltips cannot survive refreshes or rule edits.
- Added Whitelist to the custom truncated-cell hover tracker so its ID, ID Filter and address behavior matches Blacklist.
- Lane's cascade menu now explicitly uses Semaphore's **Anonymous Pro, bold, 17 pt** typography instead of falling back to the Windows/Arial menu font.
- All painted traffic/policy/manual badges now use the same **1 px white border** as Semaphore's inner table-cell borders; removable Port/ID Filter popup badges use the same border treatment.
- Reworked long-input edge fading around Qt's actual horizontally scrolled content range, using `cursorPositionAt()` plus caret/scroll geometry in the same spirit as MJTC's real content-host fade rather than a purely estimated text rectangle.
- The fade mask now starts at the actual inside edge of the line-edit frame, fully covers style padding where Qt can paint partial glyphs, reaches a fully opaque background at the clipped edge, and transitions to transparent over the visible text.
- Fade background colors now match Semaphore's actual input surfaces, including the inline policy-ID editor's normal and gold focus/hover states, eliminating the residual edge fragments produced by mismatched QSS/palette colors.

### Window minimum, badge-border, Whitelist-font, Country-tooltip and bidirectional input-fade corrections

- Hardened the **999 px** main-window minimum so it is enforced by one canonical `999x520` constant set across Qt sizing, Win32 `WM_GETMINMAXINFO`, resize events, restored Qt geometry and native `SetWindowPos` tray restores.
- Legacy/saved placements smaller than the new minimum are now clamped or rejected instead of being able to restore Semaphore below 999 px wide after startup or tray restore.
- Badge rendering now separates the smooth rounded fill from a **non-antialiased, cosmetic 1 px pure-white outline**, giving traffic, D&T, Protocol, policy and manual-policy badges the same high-contrast stroke weight as inner table-cell borders instead of a gray antialiased fringe.
- Restored the Whitelist table body to **Anonymous Pro, bold, 12 pt** and its header to **Anonymous Pro, bold, 17 pt**, preventing a native/Arial fallback in late-created Whitelist views.
- Country flag tooltips no longer append `Click to move this country...` or blocked-policy action/status prose; only the base country/location tooltip remains.
- Rebuilt QLineEdit overflow-side detection from Qt's live caret position and the width of the text prefix, so hidden-left and hidden-right states are calculated independently as the caret scrolls through long input.
- Protocol search now places the right fade at the actual text viewport edge before the embedded filter glyph, rather than underneath the glyph at the outer line-edit frame.
- When the caret is moved back through a long value with the arrow keys, the right edge now gains its own opaque guard + alpha fade while the left edge remains faded whenever text is still hidden there.

### Badge geometry, empty-cell hatch, input-caret fade and 1280 px minimum

- Raised the v1.1.1.1 main-window minimum width from 999 px to **1280 px** while preserving the 520 px minimum height and the existing Qt/Win32/startup/tray enforcement paths.
- Cell badges no longer use rounded corners: fills and outlines are now square, non-antialiased rectangles aligned to the table grid.
- Normal badge outlines remain crisp 1 px white; hovered/selected badge outlines now switch to the same color as the badge text (black on the gold hover/selection state), so border and text respond as one visual state.
- Empty-cell parallel hatching now uses black 1 px lines instead of white, preserving the existing 1 px line / 1 px gap density.
- Corrected the long-input fade endpoint edge case where returning the caret to character 0 could leave a stale left fade because QLineEdit hit-testing rounded the leftmost pixel to position 1. Caret-at-start/end now authoritatively clears the corresponding fade.
- The edge-fade overlay now excludes Qt's native insertion-caret rectangle, so the blinking cursor pipe keeps full contrast and is never alpha-faded by the overflow mask.

### Empty-cell hover hatch and input-caret artifact correction

- Restored empty-cell parallel hatching to **white** in the normal state; only direct cell hover switches the hatch to **black** for contrast against the gold hover background.
- Selection without hover no longer forces the hatch black.
- Removed the cursor-rectangle hole from the QLineEdit alpha-fade overlay. That hole exposed moving strips of underlying glyph pixels as the caret blinked/moved and caused the corruption visible in long Protocol/input values.
- The fade now remains continuous across the full text surface and redraws only a one-pixel blinking insertion pipe above the mask when the caret itself falls inside a faded edge, preserving cursor visibility without uncovering adjacent text.


### 2026-08-15 — 1366 px minimum, exact compact traffic widths, and input-fade/caret correction

- Raised the enforced Semaphore main-window minimum width from 1280 px to 1366 px while retaining the 520 px minimum height; the shared minimum remains authoritative for Qt sizing, native `WM_GETMINMAXINFO`, resize correction, startup restore and tray/native restore paths.
- Reworked compact live-traffic column sizing across Outbound, Inbound and Through so non-stretch metadata columns use the same left/right geometry as their actual delegate content instead of retaining one-sided trailing safety margins.
- Removed the former 12 px badge-width safety tail; D&T and Protocol badge widths now mirror their rendered three-pixel outer margins, badge padding and inter-badge spacing directly.
- Plain compact traffic cells now size from the delegate's actual two-pixel left/right text inset, and repeated-address cells reserve only the space actually consumed by the `+N` counter and its separator.
- Compact traffic columns are now allowed to shrink as well as grow when widths are initialized/restored, preventing stale historic widths from leaving large blank tails after content changes.
- Clearing a traffic table resets all compact sections to current header geometry so the next row grows from its real content width; fresh profiles with no saved traffic history receive the same initialization.
- Preserved the first-column reload hit target while reducing its unrelated right-side padding.
- Fixed false left-edge input fading when moving the caret only one or two characters from the start of a long value: fade activation now follows the reconstructed QLineEdit horizontal scroll only, without the previous eager cursor hit-test fallback.
- Removed the synthetic manually redrawn caret that could produce two visible insertion pipes. The native Qt caret is preserved through a narrow 1–2 px exclusion in the fade clip, avoiding both caret fading and the former wide glyph-reveal artifact.

### 2026-08-15 — traffic content-fit correction, From/To headers, and caret-safe input fading

- Corrected the over-tight compact traffic-column calculation introduced by the previous exact-fit pass. Plain cells now retain the delegate's symmetric 2 px text insets plus a 2 px grid/font-metrics guard, and badge columns retain a 2 px symmetric rendering guard; this prevents `#`, D&T, local endpoint, Port and Protocol values from being elided when their measured text nominally equals the section width.
- Width measurement now takes the larger of `horizontalAdvance()` and the rendered font bounding width, covering glyph side bearings at Windows fractional DPI while keeping the visible left/right margins effectively symmetric instead of restoring the former large trailing safety tail.
- Applied the corrected measurements to startup/restored-history scans and live-row growth across Outbound, Inbound and Through.
- Renamed every live traffic header from **Origin** to **From** and **Destination** to **To**. Detail/history views that derive labels from the source table inherit the same terminology.
- Increased the QLineEdit overflow-scroll activation tolerance so moving only a few characters from the start cannot create a false left fade before the text has actually scrolled.
- Removed caret-region clipping from the fade overlay. When the native caret reaches an edge-fade region, that fade now terminates immediately before/after the caret instead of punching a transparent stripe through already-rendered text, preventing the recurring double-pipe/glyph-stroke artifact while leaving Qt solely responsible for caret drawing and blink timing.

### Header terminology and final input-fade edge cleanup

- Shortened policy-table headers from `First IP Range` / `Last IP Range` to `First IP` / `Last IP`.
- Shortened displayed protocol headers and the Protocol selector's integrated placeholder from `Protocol` to `Proto`.
- Reworked the final caret/fade boundary case so no antialiased tail from the next hidden character can remain visible beyond the insertion pipe.
- Removed the permanent caret-shaped transparency from the fade; when the caret reaches an active fade, Semaphore fully masks the hidden side, covers the native caret locally, and redraws exactly one 1 px caret using the configured Qt blink cadence.


### Input overflow fade and mixed counted-row history

- Fixed the edge-fade/caret interaction so the fade no longer erases every character between the viewport edge and the caret before the caret actually reaches the boundary.
- Complete visible characters remain intact while navigating overflowing inputs; only the platform caret pixels are replaced inside an active fade to prevent a hidden neighbouring glyph tail from leaking past the insertion pipe.
- Added a per-iteration allowed/blocked result snapshot to folded `+N` traffic history.
- Counter-detail modals now preserve mixed results inside one aggregated row instead of applying the newest/last packet color to every historical iteration.
- Outbound and Inbound use each packet's own result; Through preserves independent From/To endpoint results and derives Proto from either endpoint being blocked.
- Advanced persisted traffic iterator data to version 13 so per-iteration result colors survive restart while retaining compatibility with older history formats.
- WFP classify-drop reconciliation now updates the matching newest iteration snapshot as well, so an authoritative blocked result cannot leave that individual modal entry green.

### Input fade navigation stabilization

- Reworked overflowing QLineEdit edge fading so the overlay no longer masks, replaces, clips around, or manually redraws the insertion caret at any stage.
- Removed the custom fade-caret blink machinery entirely; Qt is again the sole owner of caret placement and blink state.
- Removed the opaque edge guard that could hard-clip a character while QLineEdit scrolled horizontally; the alpha gradient now reaches fully opaque exactly at the viewport boundary and transitions smoothly inward.
- When the native caret approaches an active left/right fade, only that fade is shortened by a small clearance so the caret and the complete adjacent visible glyphs remain untouched.
- Preserved independent hidden-left/hidden-right detection from the reconstructed QLineEdit horizontal scroll state, including the existing start/end safeguards.

### Video-verified input-fade navigation correction

- Reviewed the recorded Protocol-search navigation sequence frame-by-frame and confirmed the remaining defect was not the hidden-side detector itself: the fade endpoint was moving through arbitrary pixel positions while Qt simultaneously scrolled the shaped text, so the transition could land inside a glyph and visually slice/reveal character fragments.
- Replaced integer `QFontMetrics` edge positioning in the overflow-fade path with `QTextLayout` shaped-text cursor geometry, keeping fade placement aligned with Qt's actual glyph shaping and fractional-DPI cursor positions.
- Left/right fade endpoints now snap to real text insertion boundaries rather than arbitrary pixels, so the transparent end of a fade cannot terminate in the middle of a character.
- When the native caret enters an edge-fade zone, the fade ends/starts exactly at that insertion boundary with zero overlay opacity there; Qt remains solely responsible for the caret and blink state.
- Removed the prior caret-clearance gap behavior that could expose partial glyph strokes while navigating.
- Hidden-left and hidden-right detection remains independent and still follows the reconstructed live QLineEdit horizontal scroll state.
- Video-guided input-fade hardening after reproducing the remaining navigation artifact:
  - reviewed the 144 fps capture frame-by-frame rather than relying on isolated screenshots;
  - masks any partially visible edge glyph completely up to the nearest shaped-text insertion boundary;
  - begins/ends the alpha transition only on complete-character boundaries, preventing character tails from flashing while QLineEdit scrolls;
  - removes caret-dependent fade-length changes so arrow-key navigation cannot make the gradient jump around the insertion cursor;
  - preserves only Qt's exact native caret stripe when an edge overlay crosses it, without synthetic caret painting or a wide glyph-revealing hole;
  - keeps independent left/right overflow fades and the existing Protocol-filter input geometry.
- Replaced the input-fade navigation overlay with a text-layer compositor: overflowing QLineEdit text is redrawn from Qt's native cursor/scroll geometry into an off-screen alpha-masked layer, while the caret is erased from the native pass and drawn exactly once afterward. This removes the competing overlay/caret pipelines that caused sliced glyphs, double pipes and incorrect Left/Right navigation in the submitted 144 FPS videos.
- Reworked the Protocol picker search control into a native 16-character monospaced `QLineEdit`; the tri-state protocol filter is now a separate square control with its own gold border, eliminating shared text/toggle pixels and custom fade/caret repainting from that editor.
- Protocol-search caret movement, selection, clipping and horizontal scrolling are now fully native Qt behavior, preventing the prior custom fade layer from slicing glyphs or producing caret-pipe artifacts.
- Added `Update-Dependencies.bat` plus `tools/update-dependencies.ps1` to audit/update Semaphore's managed development dependencies: stable Qt packages and matching Qt/MinGW toolchain through Qt Maintenance Tool, current CMake/Ninja through WinGet when available, plus reporting for Windows PktMon and project-managed resource dependencies. Preview/beta/RC Qt releases are explicitly excluded.
### Dependency-updater PowerShell parser correction

- Fixed the new dependency updater failing before execution under Windows PowerShell because `$rc:` inside an interpolated error string was parsed as an invalid scoped-variable reference.
- The exit-code interpolation now uses `${rc}:`, preserving the intended diagnostic while remaining valid in Windows PowerShell 5.1 and newer PowerShell versions.
- Audited the updater for the same unbraced variable-before-colon pattern; the remaining `$env:...` references are intentional PowerShell scope syntax.

- Protocol search input reworked again around a deterministic 16-cell Anonymous Pro viewport: text now advances only in whole monospaced character cells, edge fades are applied only at character-aligned overflow boundaries, and a single custom blinking caret is painted last on an exact insertion boundary so no glyph can be hard-clipped by the pipe.
- Protocol filter toggle moved back visually inside the search control: the search field and 29 px state square are contiguous with no gap, use the same Semaphore gold border, and share one composite input silhouette while remaining separate widgets internally so the toggle cannot steal text/caret pixels.
- Protocol search width now uses floating-point font metrics rounded outward plus a DPI/glyph-overhang guard, guaranteeing room for all 16 requested monospaced characters before the integrated filter square.

- Protocol search field now keeps the tri-state toggle visually inside the input box while remaining a separate square control for crisp rendering.
- Protocol search uses a deterministic 16-character viewport with wider guards so all 16 monospaced characters fit without edge clipping.
- Protocol search overflow fading is stronger and begins around the last/first three visible characters when hidden text exists beyond the viewport.
- Protocol search caret now clears exactly one pixel column beneath the blinking pipe so the caret fully covers underlying characters without duplicated tails.


### Dependency-updater log-file locking correction

- Fixed `Update-Dependencies.bat` failing during the Qt Maintenance Tool check because `Start-Transcript` and `Tee-Object` attempted to write the same `dependency-update-*.log` file concurrently under Windows PowerShell.
- `Start-Transcript` is now the single owner of the dependency log; native command output is captured first and replayed through `Write-Host`, so it is still recorded in the transcript without opening a competing file handle.
- Removed the second direct log writer from the Qt package-search path for the same reason.
- Command exit codes are captured immediately after the native process returns, before replaying its output, preserving reliable failure handling.

- Build warning cleanup: removed the unused `baseline` variable from the Protocol search renderer, eliminating the GCC `-Wunused-variable` warning.
- Portable build now suppresses only QtGui's known optional `WrapVulkanHeaders` CMake STATUS line while leaving every other CMake warning/error visible. Semaphore does not link Vulkan support.
- `windeployqt` now explicitly opts out of the unused system DXC compiler probe (`dxcompiler.dll` / `dxil.dll`), eliminating the irrelevant Direct3D 12 deployment warning.
- `windeployqt` now explicitly excludes `qopensslbackend`; Semaphore keeps Qt's Windows Schannel and certificate-only TLS backends, avoiding the optional OpenSSL-probe warning without adding an unnecessary OpenSSL runtime dependency.

## Final release hardening after the build/tooling cleanup

### Policy editing and normalization

- Manual Blacklist/Whitelist field edits now re-enter the canonical rule-reconciliation path instead of only changing the visible cell value.
- Address-only rules that become scoped through Lane/Proto/Port/ID Filter edits are separated into standalone scoped rules, while rules edited back to equivalent address-only scope can rejoin the optimized range store.
- Compatible edited rules can deduplicate/merge without discarding their retained IDs/provenance.
- ID edits trigger canonical deduplication after the editor commits.
- Newly arriving traffic selector cells resolve their logical Allow/Block state before first paint instead of briefly exposing an internal neutral/pending gray state.

### Typography, controls and editable-field rendering

- Removed affected native/default-font fallbacks and standardized Semaphore-created policy dialogs, menus, controls and editors on the existing **Anonymous Pro** family without shrinking their intended point sizes.
- Corrected the manual `+` Protocol selector and ID Filter typography so nested popup content no longer falls back to Arial/default UI fonts or a reduced-looking size.
- Refined the Protocol filter control into a compact in-field control with complete borders and a check mark matching Semaphore's ordinary checkbox style.
- Reworked reload glyphs so their circular arrow geometry renders completely at normal and hover states.
- Manual policy ID editing keeps a deterministic visible viewport while permitting longer stored IDs through the existing overflow behavior.
- Inline ID editors use high-contrast black text on the gold edit surface and the established dark selection treatment where applicable.
- Live traffic ID editing preserves its badge/editor visual treatment and selection colors rather than introducing a second unrelated native editor style.
- Removed the `Lists / policy` helper wording in favor of the shorter **Rules** tooltip.

### Long-input navigation/caret hardening

- Reworked long-input horizontal overflow handling around Qt's real line-edit geometry and native scrolling behavior.
- Eliminated competing text/caret paint paths that produced halos, duplicated insertion pipes, partial glyph tails and discolored text around the caret.
- Edge fading is now applied without moving the beginning of a value merely because the caret moved one character from the start.
- Long manual-rule and inline policy editors preserve full-field editing while revealing genuinely hidden text only at the active overflow edge.

### GeoIP, validation and build diagnostics

- `Customize-GeoIP.bat` now leaves a failed customization session visible, reports the failed stage and exit code, and waits for confirmation instead of closing before the diagnostic can be read.
- Refreshed `tools/validate-source.py` away from obsolete development-token checks and aligned validation with the current v1.1.1.1 source structure.
- Fixed validator ordering/scope errors that could raise Python exceptions before current-source checks completed.
- Preserved successful City, ASN, flag-pack and manifest generation while making validation failure reporting explicit.

### Compile fixes

- Corrected the custom-caption maximize-button cast when the stored button is a `QPointer<QPushButton>`.
- Corrected a `QColor selectedText` local variable that shadowed `QLineEdit::selectedText()` in the live ID editor renderer.
- These fixes are source-only corrections; they do not change the release-version comparison or WFP policy semantics.


---

# Semaphore v1.1.1 — Exhaustive changes since v1.1

This changelog is intentionally exhaustive for the v1.1 → v1.1.1 development cycle.

## Added

- Local ASN organization lookup for public IPv4/IPv6 endpoints using packaged MaxMind GeoLite2 ASN data.
- Compact runtime ASN organization data generated for Semaphore instead of performing per-address online organization lookups.
- Automatic endpoint ID/name assignment from ASN organization data when no higher-priority identity exists.
- Automatic propagation/refresh of generated endpoint identities across applicable traffic and policy views.
- Manual-ID preservation so user-entered identities remain authoritative over generated identities.
- Deterministic generated-identity precedence: manual ID/name → well-known/special-purpose identity → ASN organization → `Unnamed`.
- Built-in recognition of applicable well-known and special-purpose IPv4 ranges.
- Built-in recognition of applicable well-known and special-purpose IPv6 ranges.
- Descriptive identification for recognized multicast, link-local, loopback/local and scoped multicast traffic where applicable.
- Special-purpose identity handling that takes precedence over a generic ASN organization where the local/network role is more useful.
- Local special-purpose/ASN identity generation without adding an external address-lookup API.
- Unified Blacklist/Whitelist policy representation for simple and scoped rules.
- Lane/direction as an explicit policy dimension.
- Protocol as an explicit policy dimension.
- Port as an explicit policy dimension.
- Country scope as part of the normalized policy representation.
- ID as a distinct human-readable policy/endpoint field.
- ID Filter as a distinct matching field separate from ID.
- Protocol selector support for the IP protocol-number space and applicable protocol names.
- Separate IPv4/IPv6 protocol identities where applicable, including TCPv4/TCPv6 and UDPv4/UDPv6.
- Explicit `Any` protocol/Port policy state.
- Explicit `None` protocol/Port state that intentionally matches nothing instead of behaving as a wildcard.
- Scoped policy enforcement plumbing from GUI policy rows into the effective WFP policy path.
- Policy normalization shared by Blacklist controls, Whitelist controls, live traffic actions, traffic-history actions, restored persisted rules and rule edits.
- Exact duplicate policy collapse.
- Compatible address/range merge handling that preserves all other policy dimensions.
- Compatible adjacent/overlapping Port-range coalescing when every other scope dimension is equivalent.
- Multi-value ID Filter storage.
- `*` wildcard support in ID Filter values.
- `?` wildcard support in ID Filter values.
- OR semantics between multiple ID Filter values in the same rule.
- Badge-based ID Filter editor.
- Removable `×` controls for individual ID Filter badges.
- Compact scrolling for ID Filter editors containing more values than the visible editor height.
- ID Filter rule merging by unioning filter values when every other policy dimension is equivalent.
- Complete composite-policy summary on ID hover.
- Policy-summary badges for action, Lane, Protocol, Port, ID Filter, Country and address scope where applicable.
- Compact badge rendering for Blacklist/Whitelist Protocol values.
- Compact badge rendering for Blacklist/Whitelist Port values.
- Compact badge rendering for Blacklist/Whitelist ID Filter values.
- Compact monitor-table badges for D&T.
- Compact monitor-table badges for ID.
- Compact monitor-table badges for Protocol.
- Content-sized monitor badges instead of full-cell-width badge backgrounds.
- Adaptive badge typography so values that previously fitted are not unnecessarily truncated by badge padding.
- Reduced Through-table badge typography for dense timestamp/protocol values.
- Smooth antialiased diagonal empty-value marker for applicable empty monitor/policy cells.
- Explicit exclusion of empty ID Filter cells from the diagonal empty-value marker.
- Explicit full-value tooltips for truncated Blacklist/Whitelist address/range cells.
- WFP classify-drop telemetry for traffic blocked by Semaphore-owned WFP filters.
- Semaphore-owned runtime filter-ID validation before a WFP drop event is surfaced to the GUI.
- Private broker-to-GUI blocked-event telemetry over the existing privileged communication path.
- Blocked-event reconstruction when the ordinary packet-capture path never receives a successfully blocked packet.
- Direction-aware blocked-event insertion into Outbound/Inbound traffic views.
- Persistent arrival-time policy-state snapshots for traffic history.
- Expanded persisted traffic-history payload for richer iteration-modal data.
- Expanded traffic-iteration popup columns with the applicable remote endpoint, Port, Flag, ID/name and Protocol.
- SVG flag rendering inside the traffic-iteration popup.
- Per-iteration ID/name retrieval rather than substituting only the current canonical identity.
- Complete-row table viewport rendering.
- Suppression of partial bottom rows until their complete row height fits.
- Suppression of partially positioned top rows.
- Row/item-aligned vertical scrolling for tables.
- Complete-row Country tile rendering at the bottom of the viewport.
- Country-page vertical reflow tied to the actual visible complete-tile area.
- Settings cog at the top tab level.
- Production release/update checking for newer public Semaphore releases.
- Version-aware update comparison so only a genuinely newer release produces the normal update notification.
- Custom release/update popup integrated with Semaphore's visual language.
- Native rounded-region handling for custom popups/menus where required to eliminate square backing corners.
- Native Windows title-bar move-loop integration for the custom title bar.
- Native edge/corner resizing for all four edges and four corners.
- Qt native `startSystemResize()` use with Win32 fallback where required.
- Smaller practical minimum window geometry while preserving the normal larger startup size.
- Persistent startup restoration for actual last usable window position/size/state.
- Generated-ID/name refresh after restored policy/identity data becomes available.
- Build-wrapper pause/inspect behavior for failed builds where applicable.
- Validator support for the generated ASN organization resource/data path.
- Qt 6.11.1-specific compile/validation repairs introduced by the new policy and viewport code.

## Changed

- Blacklist and Whitelist remain unified pages instead of retaining the temporary Absolute/Scoped split explored during v1.1.1 development.
- Policy controls were reorganized around the unified table instead of a separate permanent right-side action panel.
- Rule identity generation now describes all active policy dimensions instead of only the most recently edited field.
- Legacy auto-generated IDs are recognized as generated values so they can be refreshed when rule scope changes.
- Manual IDs are distinguished from generated IDs so editing policy scope does not overwrite deliberate user text.
- Existing legacy Name/ID rules are migrated toward explicit editable address bounds instead of ambiguous `Any / Any` scope.
- Legacy generic TCP/UDP history/policy values are migrated according to the row/rule address family where possible.
- Protocols are represented individually instead of being grouped into broad TCP/UDP families.
- Protocol matching differentiates address family where appropriate.
- `None` is treated as a disabled match condition instead of an unrestricted selector.
- Port matching uses the same normalized policy path as address, protocol and other rule dimensions.
- Policy insertion from GUI actions now runs through the same deduplication/canonicalization path as persisted/startup policy.
- Port policies are coalesced only when every non-Port scope dimension matches.
- ID Filter values are maintained separately from the human-readable ID field.
- Empty ID Filter selection/commit no longer writes `Unnamed`.
- Selecting/editing an ID Filter without actually changing data no longer triggers unnecessary `setData()`, merge or WFP reconciliation work.
- Otherwise-equivalent ID Filter rules merge by filter-set union rather than leaving duplicate policy rows.
- Composite generated policy IDs update as Protocol, Port, Lane, Country or ID Filter scope changes.
- Hover inspection is used to expose complete composite policy rather than forcing every scope value into the visible ID text.
- Outbound table ordering was normalized around the blockable remote endpoint and associated policy metadata.
- Inbound table ordering was normalized around the blockable remote endpoint and associated policy metadata.
- Traffic-history iteration layouts were updated to place endpoint-specific data together and include richer metadata.
- Traffic history format was advanced to carry the expanded iteration/policy snapshot data while retaining interpretation of older stored history.
- Traffic-row red/green state now relies on recorded arrival-time policy snapshots for historical entries.
- Current live state and historical state are resolved separately instead of repainting all previous traffic from today's policy.
- WFP blocked-event direction is derived from the actual classify-drop/filter direction rather than an over-constrained transport-side comparison.
- WFP drop telemetry is correlated only with Semaphore-owned filters.
- Effective GUI block state is derived from normalized/current WFP policy rather than preserving retired ranges in a stale cache.
- Whitelist/Allow display resolution uses the same specificity ordering as effective enforcement instead of treating any intersecting Allow rule as an override.
- Mixed/partial policy coloring uses normalized address/protocol/Port/permit precedence.
- First unblock action from historical red cells now creates the required Allow/Whitelist exception immediately.
- Port/Protocol/ID policy-cell unblock actions follow the same first-action exception behavior.
- Coalesced Port policies are respected during unblock so a historical Port cell does not immediately recreate the block it just removed.
- Blacklist/Whitelist range coverage logic was aligned with the effective policy scope rather than treating every address intersection as equivalent.
- Country-derived coverage participates in the same normalized effective policy system as other rules.
- Country scrolling remains aligned to complete flag rows during wheel, arrow, page, thumb and resize interaction.
- Country viewport rendering recalculates from the complete visible tile geometry.
- Table viewport rendering changed from ordinary Qt partial-row painting to complete-row painting.
- Table scrolling changed to item/row increments where required for complete-row guarantees.
- Bottom-scroll behavior was adjusted so resizing/scrolling cannot leave clipped partial rows.
- ID Filter editing remains functional under the custom delegates used for complete-row/policy rendering.
- Monitor D&T / ID / Protocol badge rectangles shrink-wrap their actual text content.
- Badge text uses adaptive font reduction where padding would otherwise create a new ellipsis.
- Through badges use slightly smaller typography than the other monitor views for dense values.
- Applicable empty values use a smooth diagonal line rather than the previous rigid empty-cell style.
- The diagonal marker uses antialiasing, fractional cosmetic width and smooth cap/join behavior.
- Empty Blacklist/Whitelist ID Filter cells remain blank.
- Counter-bearing IP cells use ordinary ellipsis instead of a fade that obscures the address.
- Counter text remains visible without adding a separate dark backing rectangle.
- Full IP values remain available through hover tooltips when counters or narrow columns cause elision.
- Window dragging uses the native Windows move operation rather than only custom manual geometry movement.
- Window resizing uses native edge/corner behavior while retaining the custom frame.
- The startup size remains large while the minimum size is lower, allowing inward resizing that v1.1.1 development builds initially prevented.
- Title-bar hit testing was refined so movement does not consume button/control interaction.
- Maximize, restore, double-click and Windows Snap behavior are preserved through the native movement/resizing path.
- Actual last window placement is stored/restored instead of restoring to a generic center/default after tray use or resize.
- Custom popup/menu geometry was changed to use an actual rounded native region where the backing HWND would otherwise reveal black square corners.
- Release-check production behavior was simplified to notify only for an actually newer release.
- Startup restoration orders policy, generated identities, window geometry and release checking so one does not overwrite another.
- The main version identity/badge moved from v1.1 to v1.1.1.

## Fixed

- Public IPs remaining `Unnamed` even though a local ASN organization could identify them.
- Generated organization identities not propagating consistently to other tables containing the same endpoint.
- Automatically generated identities overriding a manual user identity.
- Generic ASN organization labels being used where a more useful well-known/special-purpose network identity should take precedence.
- Special-purpose IPv4/IPv6 traffic lacking meaningful local identification.
- ASN generator/validator disagreement even when the generated runtime ASN database itself was valid.
- Header/baseline declaration damage introduced during early organization-auto-name overlays.
- Legacy generated IDs becoming indistinguishable from genuinely manual IDs.
- Generated rule IDs changing to only the newest ID Filter and silently omitting existing Protocol/Port/Lane/Country scope.
- Legacy Name/ID rules displaying ambiguous `Any / Any` address scope after migration.
- Scoped policies being represented in the UI without equivalent enforcement state.
- Scoped WFP filters not consistently contributing to the GUI's current blocked/allowed status.
- Protocol/Port selector popup behavior and clipped custom checkbox/tick rendering.
- `None` Protocol/Port values accidentally behaving like unrestricted rules.
- Protocol-family grouping that prevented independently editable TCPv4/TCPv6 or UDPv4/UDPv6 policies.
- Legacy protocol strings failing to migrate cleanly to family-specific values.
- Duplicate policies created through different UI paths.
- Adjacent/overlapping Port policies remaining unnecessarily fragmented.
- Port-range merging that could discard or ignore non-Port scope if performed too aggressively.
- First right-click/unblock action on historical blocked cells failing to create the needed Allow exception.
- Historical Port `80` inside a coalesced `80-81` block immediately recreating Port `80` instead of remaining unblocked.
- Port/Protocol/ID policy-cell actions using inconsistent unblock semantics.
- Empty ID Filter fields being converted to `Unnamed`.
- Shared ID/ID Filter editor behavior applying ID's empty-value rule to ID Filter.
- Selection-only ID Filter interactions causing policy mutation/reconciliation.
- Multiple otherwise-equivalent ID Filter policies remaining as duplicate rows instead of merging their filter values.
- ID Filter editor inability to retain several simultaneous wildcard values cleanly.
- Rule-summary hover omitting existing Protocol/Port/Lane/Country constraints after another filter was added.
- Blacklist/Whitelist long address values having no reliable full-value tooltip when visually truncated.
- Incorrect hard-coded tooltip column mapping after the policy table gained new columns.
- Blocked traffic disappearing completely because WFP dropped it before the ordinary Packet Monitor path could observe it.
- Broker drop telemetry accepting/handling events without sufficiently tying them to Semaphore-owned runtime filter IDs.
- Race conditions between blocked-event telemetry and ordinary capture presentation.
- Duplicate/incorrect blocked rows caused by overlapping telemetry paths.
- Outbound blocked rows being filtered out by an incorrect direction comparison introduced by scoped-rule handling.
- Inbound/Outbound direction derivation being too restrictive when the WFP classify-drop event and runtime filter direction were both relevant.
- Blocked-query rows failing to remain visible/red even though enforcement itself was working.
- Traffic-cell status using current policy alone and thereby repainting old observations incorrectly.
- Historical rows turning red after a later Blacklist/Country change even though they were allowed when observed.
- Historical rows turning green/red incorrectly after later Whitelist edits.
- Missing persisted arrival-time policy state across restart.
- Traffic-history popup payload lacking Flag, ID/name and Protocol information for individual iterations.
- Expanded history payload being interpreted incorrectly by older stored-history layouts.
- Country policy actions and traffic-cell colors disagreeing with effective policy.
- Broad Allow rules producing a false mixed/purple state even when a more-specific Block wins.
- Range coverage calculations treating partial/overlapping scope as a complete unconditional block.
- GUI state remaining red after WFP had successfully retired the obsolete block rule.
- Retired ranges being removed from a worker's confirmed set but then resurrected in the GUI `appliedRanges` cache.
- `isIPBlocked()` returning true from stale cache state after network access had already been restored.
- Critical WFP reconciliation paths failing to retire/update the intended scoped filter set correctly.
- Rule retirement and subsequent GUI refresh reintroducing obsolete effective address coverage.
- Modal traffic actions diverging from equivalent actions initiated in the main policy table.
- Country and range actions failing to reuse the canonical policy normalization path.
- Existing traffic not being marked/updated correctly when a newly applied policy attempted to cover it.
- Compile failure from the missing/declaration-mismatched `markExistingTrafficAttemptBlock` path.
- Custom title-bar dragging not entering a real native move loop.
- Title-bar movement interfering with expected Snap/maximize/restore behavior.
- Manual edge/corner resizing appearing broken because the startup size was also being used as the minimum size.
- Edge/corner resize handling working once and then becoming unreliable because of stale border/input state.
- Custom-frame hit testing preventing repeated resize operations.
- Window placement restoring to the wrong position after tray/minimize/resize sequences.
- Startup resize/placement logic overwriting the intended restored position.
- Startup-generated IDs not refreshing after the supporting ASN/special-purpose data became ready.
- Settings/cog startup state not being restored in the intended order.
- Temporary release-check test state interacting with real release-tag suppression.
- v1.1 being presented as an update over a v1.1.1 development build during release-check testing.
- Release modal title/geometry inconsistencies introduced by test-mode styling.
- Square black backing corners around visually rounded release/menu windows.
- Popup/menu maximum viewport sizing leaving content clipped or misaligned.
- Broker telemetry build/compile issues introduced by the WFP-drop IPC path.
- Build command windows disappearing before a failure could be inspected in the wrapper workflow.
- Partially visible table rows at the bottom of traffic/policy views.
- Partially positioned rows at the top after pixel-style scrolling.
- Mouse interaction targeting a row that was only partially visible.
- Country flags being sliced at the bottom during manual scrolling or vertical resize.
- Complete-row viewport code compile incompatibilities under Qt 6.11.1.
- Bottom-scroll calculations leaving a clipped last row after a resize.
- ID Filter editing breaking after the complete-row/custom delegate changes.
- Protocol/Port rules failing to merge after edits that made their complete scope equivalent.
- Port and Protocol rule merge paths failing to preserve the rest of the policy dimensions.
- ID Filter selection turning an intentionally empty filter into `Unnamed`.
- Policy ID text being rendered as a badge even though it needs ordinary editable text.
- ID cells losing ordinary ellipsis/direct-edit behavior after badge delegates were introduced.
- Protocol/Port badge overflow hiding additional values instead of retaining the `+N` behavior where applicable.
- Monitor badges stretching across the entire cell instead of fitting their contents.
- D&T/Protocol values becoming newly truncated solely because badge padding was added.
- Through-table dense badge text touching/exceeding the badge contour.
- Empty policy/monitor cells using an overly rigid line instead of a smooth diagonal marker.
- Empty ID Filter cells receiving the diagonal marker even though blank is semantically clearer.
- Counter-bearing IP cells using a fade that unnecessarily obscured otherwise readable address text.
- Counter/address tooltips failing to expose the complete elided value consistently.
- Stale source/validator warnings and compile mismatches introduced during successive v1.1.1 overlays.

## Removed / stripped

- Dependence on an online ISP/organization lookup service for automatic endpoint identification.
- Need to issue a network request for every new public address merely to obtain an organization name.
- Temporary Absolute/Scoped Blacklist/Whitelist page split explored during early v1.1.1 policy development.
- Temporary permanent right-side policy action-panel concept after the unified policy-table design was adopted.
- Broad protocol grouping that hid individual protocol/family identities.
- Treating `None` as equivalent to `Any`.
- Duplicate policy insertion paths that bypassed canonical normalization.
- Redundant exact duplicate rules.
- Redundant compatible Port fragments after Port-range coalescing.
- Coupling of the human-readable ID field to ID Filter's empty-value behavior.
- Automatic conversion of an empty ID Filter to `Unnamed`.
- Single-value limitation for ID Filters.
- Requirement to inspect only a generated ID string to understand a composite rule.
- Assumption that any intersecting Allow rule necessarily creates a partial/mixed state.
- Requirement for a second unblock attempt when the first action should create a Whitelist exception.
- Dependence on ordinary packet capture as the only way to display traffic blocked by Semaphore.
- Stale retired-rule entries in the GUI's applied-range cache.
- Pixel/partial-row table presentation at viewport boundaries.
- Partial Country flag rows at the bottom of the viewport.
- Full-cell-width monitor badge backgrounds.
- Fade-based address truncation in counter-bearing cells.
- Diagonal empty marker from the ID Filter field.
- Temporary release-check test shortcuts/modes used during v1.1.1 development.
- Temporary development/update-state labels that are not part of normal stable-release behavior.
- Square native backing corners around rounded custom release/menu surfaces.

## Preserved

- Driverless Windows Packet Monitor capture architecture.
- Direct Windows Filtering Platform hard-block enforcement.
- Non-elevated Qt GUI / elevated broker privilege separation.
- Private IPC between GUI and privileged networking component.
- WFP/Packet Monitor duplicate-correlation architecture.
- Existing live Outbound, Inbound and Through table model.
- Existing bounded live-traffic presentation/history policy where applicable.
- Unlimited Blacklist/Whitelist table presentation introduced in v1.1.
- v1.1 large-list numeric sorting/merging optimizations.
- v1.1 batched list materialization and table-item reuse.
- v1.1 durable blacklist import checkpoints and restart recovery.
- Preservation of original imported blocklist sources.
- Detailed parse → optimize → materialize → save → WFP progress reporting.
- Bounded/background WFP reconciliation.
- Priority handling for interactive policy changes.
- Stale-operation invalidation and retry handling.
- Safe delete/purge behavior while reconciliation is active.
- IPv4 and IPv6 support.
- Local GeoIP city/country lookup architecture.
- Embedded/vector country flag architecture.
- Native flag aspect ratios.
- Country-based policy.
- Whitelist precedence/exception capability.
- Persistent Semaphore state under Local AppData.
- Repeated-address counters and per-event history.
- Saved manual endpoint identities.
- Complete clipboard export behavior introduced in v1.1.
- High-rate capture/accounting decoupled from bounded GUI painting.
- Custom Semaphore title bar.
- Windows Snap, maximize and restore behavior.
- System-tray operation.
- Qt 6.11.1 portable Windows build target.

---

# Semaphore v1.1 — Exhaustive changes since v1

This changelog is intentionally exhaustive for the v1 → v1.1 development cycle.

## Added

- Unlimited Blacklist/Whitelist table presentation.
- Dynamic list `#` column width based on final row count.
- Flag column between Name and First IP Range in Blacklist and Whitelist.
- Exact full-range GeoIP flag classification.
- List flag hover tooltips.
- Country-row wheel snapping.
- Complete column/selection clipboard export.
- Detailed second-pass WFP progress reporting.
- Persistent large-blacklist import checkpoints.
- Persistent parse byte offsets and parsed-range state.
- Persistent optimization-complete state.
- Persistent materialization row cursor.
- Persistent WFP confirmed-range recovery state.
- Startup reconstruction of the bottom import/progress surface.
- Persistent import state under `%LOCALAPPDATA%\Semaphore\blacklist\import-resume\`.
- Migration support for compatible older runtime-located import checkpoints.
- Defensive preservation copy for a selected blacklist source.
- Adaptive zero-delay capture presentation queue.
- Single-pending-event GUI drain scheduling.
- Bounded GUI drain time budget under packet bursts.
- Coalesced repeated traffic presentation updates.
- Additional Windows icon size frames.
- Visible `v1.1` version badge.

## Changed

- Large-list sorting precomputes numeric IPv4 keys.
- Range merge paths reduce unnecessary copying.
- Import vectors reserve capacity based on source size.
- List materialization reuses existing table items where possible.
- List materialization runs in bounded batches.
- Whitelist uses the same large-table optimizations.
- List row layout uses fixed geometry and no word wrapping.
- Blacklist/Whitelist use 40 px rows.
- Through is restored to 24 px rows.
- Outbound stretches Destination + Name.
- Inbound stretches Origin + Name.
- Through stretches Origin + Destination.
- Tray width follows actual content more closely.
- Country scrolling advances by complete flag rows.
- Import progress covers parse → optimize → materialize → save → WFP.
- WFP retries/reconciliation remain visible in the progress surface.
- Import source is treated as read-only and preserved.
- Capture ingestion is immediate while GUI painting is adaptive.
- Packet-history hot-path handling avoids repeated complete decode/re-encode.
- Import source unavailability pauses instead of discarding the transaction.
- Startup restores progress synchronously.
- Version identity moved from v1 to v1.1.
- Application icon has higher contrast/definition and improved small-size presentation.

## Fixed

- Blacklist/Whitelist totals diverging from a 999-row truncated table.
- Massive-list performance degradation caused by repeated address parsing and table churn.
- Progress appearing stuck during list optimization.
- List contents appearing in one sudden final strike without meaningful intermediate progress.
- Blocked-country flags receiving an unwanted yellow outline.
- Outbound/Inbound Name columns failing to stretch.
- Source blacklist files disappearing after import.
- List row-number column clipping large row counts.
- WFP policy application running without bottom progress feedback.
- Missing flag tooltips in list tables.
- Incorrect expectation that every large range should receive a flag.
- Through row height being enlarged unnecessarily.
- Clipboard copying only a partial/single cell instead of the complete selected area.
- Real-time capture being artificially restricted by a 500 ms repeated-flow throttle.
- GUI lockups after removing that throttle by separating capture/accounting from rendering.
- Per-packet queued-event flooding under download-level packet rates.
- Interrupted large blacklist loads restarting from the beginning.
- Startup failing to restore the bottom progress bar for an interrupted import.
- Import checkpoints being stored inside the disposable/versioned runtime cache.
- Checkpoints being discarded when the original source was temporarily unavailable.
- Materialization progress moving backward after restart.
- WFP recovery temporarily regressing to the materialization phase.
- GUI header/source declaration mismatches introduced during iterative patching.
- `optimizeNamedRanges` 2-argument/3-argument declaration mismatch.
- Qt 6.11 mixed-type `qBound()` overload ambiguity.

## Removed / stripped

- 999-row Blacklist/Whitelist view cap.
- Yellow blocked-country flag border.
- 500 ms repeated `source|destination` display throttle.
- Repeated IPv4 string parsing from the sort comparator.
- Unnecessary full list-cell reconstruction where cells can be reused.
- Unnecessary list word wrapping.
- Unbounded/per-packet Qt presentation event pressure.
- Repeated full history decode/re-encode in the unrestricted capture hot path.
- Session-only large-import recovery.
- Runtime-cache location for durable import checkpoints.
- Silent deletion of a valid checkpoint on temporary source unavailability.
- Missing-progress gap between list construction and WFP application.
- Excess tray-menu horizontal padding.

## Preserved

- Driverless Windows Packet Monitor capture architecture.
- Direct Windows Filtering Platform hard-block enforcement.
- Non-elevated Qt GUI / elevated broker privilege separation.
- WFP/Packet Monitor duplicate correlation.
- Existing 999-row policy for the live traffic tables.
- Existing blacklist desired-policy vs confirmed-effective-policy distinction.
- Existing GeoIP/embedded vector flag architecture.
- Native flag aspect ratios.
- Existing persistent Semaphore state under Local AppData.
