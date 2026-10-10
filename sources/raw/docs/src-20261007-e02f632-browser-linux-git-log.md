2fffaab chore: prepare public GitHub release with privacy, URL display, and packaging updates.
f5191ff docs: align README with nodaysidle style, add AppImage packager and v0.1.0 release notes
ce36535 fix: resolve download close prompt, find bar, URL decoding, and installer issues
0323712 docs(V-10, V-1, V-4, V-6): align README and handoff with the code
9834ddc fix(V-4): never fall back to a refused temp profile directory
44ac858 fix(V-1): migrate default-browser and MIME entries on upgrade
4cb59cd fix(V-6): give pop-up windows error pages, crash pages and close keys
e678bbd fix(V-10): show "Download cancelled" after Cancel and fix the status text
06ccf12 fix(V-2): parent download dialogs to the main browser window
c7a7ab9 test(V-7): exercise tab teardown in a realized window with real WebViews
5c23cf4 fix(V-9): drop the unsafe idle destroy of closed tabs
aa5f6b7 fix(V-8): stop holding TabManager borrows across GTK calls
9570cf6 fix(V-4): do not trust a planted temp-dir profile directory
b15563e fix(V-3): retry a failed history save instead of stopping until exit
501ff06 fix(V-5): treat unique-local and link-local IPv6 as local addresses
9a179f0 fix(X-18): keep typed URL bar text when the window loses focus
e62c278 docs(X-14,X-29): bring README and the agent handoff in line with the code
103afbf fix(X-26): use the application ID as Wayland app_id and WM_CLASS
5a5b2c4 chore(I-1,I-2): drop the misleading mgr_weak clone, declare MSRV, add a release profile
10fbcde test(X-1): real TabManager regression test for the close-tab re-entrancy
8fbd46b fix(R-10): Home shows the built-in Home page instead of a search engine
47f8d5b fix(R-9,I-3): scope the dark window background to the browser's windows
34dc2fd fix(R-8): honest permission prompt wording and per-session decisions
6657345 fix(X-25,X-26): consistent app identity, window icon and a safer installer
8cb7a5f fix(N-2): keep the lone Home tab's close button hidden at startup
c56cee1 fix(X-24,I-4): let the window shrink and tell the two Home fields apart
98a5c3e fix(X-23): add tab tooltips and a main menu with About
ffeb2e9 fix(X-21,X-27): show styled error pages for failed loads and crashed tabs
c0de218 fix(X-22): show load progress and turn Reload into Stop while loading
630f272 fix(X-20): show a secure / not secure indicator in the address bar
0827b5e fix(X-19): truncate tab titles by characters, not bytes
8d3dcb3 fix(X-17): save history atomically, privately and in batches
46eb9cc fix(X-30): use an absolute, private profile directory and report errors
f04b79e fix(X-15,R-10): resolve typed input and command-line arguments properly
71e1cf0 fix(X-28,R-2): tear closed tabs down outside the TabManager borrow
cd92c7d fix(N-2): closing the last tab replaces it with a fresh Home tab
60a0b90 fix(X-3): open sized window.open pop-ups in their own window
aaacdeb fix(R-4): present the window on re-activation and external opens
90faf73 fix(R-6,R-3,X-9): keep focus styles honest and reveal tabs after layout
4209562 fix(N-3,R-5): handle browser shortcuts in the window key-press handler
69f1d82 fix(R-7,N-4): let WebKit drive element fullscreen and restore chrome on close
5bad0da fix(N-1,R-10): cancel a download at most once and confirm before closing
09cb11d fix(R-1): replace find dialog with a find bar that never outlives its view
30f00b6 test(X-6): cover WebKit sandbox with GTK initialised
5e9b8f3 fix(X-9): add keyboard navigation and focus styles
e264341 fix(X-8,X-11,X-12,X-18): sync navigation and fullscreen state
ae39ebf fix(X-16): fall back for empty page titles
4163fda fix(X-7,X-13): prompt for downloads and permissions
363595c fix(X-6,X-10): sandbox WebKit and reuse browser state
2d2a5e7 fix(X-5): handle external URI opens
65f2683 fix(X-4): keep selected tabs visible
bb10d7d fix(X-3): open WebKit-created views in tabs
6727577 fix(X-2): persist cookies in private SQLite store
b97f828 fix(X-1): avoid tab close RefCell reborrow
dbb7bf5 docs: record pending git remote/push as deferred
ae08c40 Initial commit: nodaysidle-browser Linux port (GTK3 + WebKitGTK)
