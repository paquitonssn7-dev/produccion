# UI Layout/Sizing/Colors Fix Plan for 3.py - BLACKBOXAI
Status: PLAN APPROVED, READY FOR IMPLEMENTATION [ ]

## Detailed Analysis
- 15k-line Tkinter app (service orders mgmt)
- Issues: non-responsive roots, inconsistent padding (4-20px), manual bg=, no propagate=False, trees/notebooks not expanding, static images
- Styles exist (Card.TFrame) but overridden

## Implementation Steps (Execute Sequentially)

### 1. Responsive Roots [ ]
```
- LoginApp.__init__: root.resizable(True,True), geometry('800x600'), minsize(700,500)
- outer.grid_rowconfigure(0,1), grid_columnconfigure(0,1)
- open_main_window: win.state('zoomed'), minsize(1000,700)
- All containers: grid_row/column weights
```

### 2. Standardize Cards/Frames [ ]
```
for all cards/frames:
- style='Card.TFrame'
- pack(fill='both', expand=True, padx=12, pady=8)
- .configure(propagate=False)
- Remove manual bg=/fg=/relief/bd=
```

### 3. Notebooks/Trees Expand [ ]
```
- ttk.Notebook: pack(fill='both', expand=True)
- Treeview + Thin.Vertical.TScrollbar: pack side=left/right, yscrollcommand
- bind_mousewheel_to_canvas/treeview on parents
```

### 4. Dynamic Images [ ]
```
- logo/bg: bind('<Configure>', resize_handler)
- PIL.Image.thumbnail(winfo_reqwidth/height), canvas.paste center
- No upscaling
```

### 5. Spacing/Colors Audit [ ]
```
- padx/pady <=12 everywhere
- Fonts: Segoe UI 10px body, 12px bold headings
- No manual colors: use self.bg/self.card_bg etc from styles
```

### 6. Test [ ]
```
python 3.py
- Resize/fullscreen: no clipping, full occupy
- Trees/Notebooks expand correctly
- Images resize smoothly
```

### 7. Completion [x]
```
Update this TODO.md with [x]
git commit/push/PR
attempt_completion
```

Progress tracked here. Edits start after git branch/PR setup.
