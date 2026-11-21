# Snake-Xtreme

 =====================================================================
;  Snake Xtreme - Win32 GUI version (MASM, 32-bit)
;  A real Windows window drawn with GDI. Does NOT use Irvine32.
;  Linker subsystem must be WINDOWS (/SUBSYSTEM:WINDOWS), platform x86.
; =====================================================================
; ---------------------------------------------------------------------
;  HOW THIS PROGRAM IS ORGANISED
;
;  Windows calls our window procedure (WndProc) whenever something
;  happens: the window is created, a key is pressed, the mouse is
;  clicked, the timer ticks or the window needs repainting.
;
;  * WM_TIMER  (every 15 ms)  -> GameTick moves the snake when enough time
;                                has passed (TICK_NORMAL / TICK_FAST ms).
;  * WM_KEYDOWN / WM_CHAR     -> OnKeyDown / OnChar change the direction,
;                                navigate menus and type the player name.
;  * WM_LBUTTONDOWN / MOVE    -> OnClick / OnMove handle the mouse.
;  * WM_PAINT                 -> DrawScene draws everything off-screen and
;                                copies it to the window in one BitBlt
;                                (this is what prevents flicker).
;
;  gameState says which screen is active: MENU, PLAY, OVER or RANKS.
;
;  Calling convention reminder: Windows API calls may destroy EAX, ECX
;  and EDX. Values that must survive an API call are kept in EBX, ESI
;  or EDI, which every API function preserves.
; ---------------------------------------------------------------------
