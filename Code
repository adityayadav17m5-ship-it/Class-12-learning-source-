# Class-12 learning source
Helps for class 12 boards students
import tkinter as tk
from tkinter import ttk, messagebox
import webbrowser
import os
from pathlib import Path

class Class12BoardPrepApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Class 12 Board Prep App")
        self.root.geometry("1000x700")
        self.root.configure(bg='#2c3e50')
        
        # Sample data structure (In real app, this would come from database/API)
        self.subjects_data = {
            "Physics": {
                "1. Electrostatics": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",  # Replace with actual educational video links
                    "notes": self.get_physics_notes("Electrostatics")
                },
                "2. Current Electricity": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_physics_notes("Current Electricity")
                },
                "3. Magnetism": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_physics_notes("Magnetism")
                }
            },
            "Chemistry": {
                "1. Solid State": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_chemistry_notes("Solid State")
                },
                "2. Solutions": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_chemistry_notes("Solutions")
                },
                "3. Electrochemistry": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_chemistry_notes("Electrochemistry")
                }
            },
            "Mathematics": {
                "1. Relations & Functions": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_math_notes("Relations & Functions")
                },
                "2. Inverse Trigonometric Functions": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_math_notes("Inverse Trigonometric Functions")
                },
                "3. Matrices": {
                    "video": "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
                    "notes": self.get_math_notes("Matrices")
                }
            }
        }
        
        self.create_widgets()
    
    def create_widgets(self):
        # Header
        header_frame = tk.Frame(self.root, bg='#34495e', height=80)
        header_frame.pack(fill='x', pady=(0,10))
        header_frame.pack_propagate(False)
        
        title_label = tk.Label(header_frame, text="🏆 Class 12 Board Prep App 🏆", 
                              font=('Arial', 24, 'bold'), bg='#34495e', fg='white')
        title_label.pack(pady=15)
        
        # Main container
        main_frame = tk.Frame(self.root, bg='#2c3e50')
        main_frame.pack(fill='both', expand=True, padx=20, pady=10)
        
        # Left panel - Subjects & Topics
        left_frame = tk.LabelFrame(main_frame, text="📚 Select Subject & Topic", 
                                  font=('Arial', 14, 'bold'), bg='#34495e', fg='white',
                                  padx=10, pady=10)
        left_frame.pack(side='left', fill='y', padx=(0,10))
        
        # Subject selection
        tk.Label(left_frame, text="Choose Subject:", font=('Arial', 12, 'bold'),
                bg='#34495e', fg='white').pack(pady=(0,5))
        
        self.subject_var = tk.StringVar(value="Physics")
        subject_combo = ttk.Combobox(left_frame, textvariable=self.subject_var,
                                   values=list(self.subjects_data.keys()),
                                   state="readonly", font=('Arial', 11))
        subject_combo.pack(pady=5, fill='x')
        subject_combo.bind('<<ComboboxSelected>>', self.on_subject_change)
        
        # Topic Listbox
        tk.Label(left_frame, text="Topics:", font=('Arial', 12, 'bold'),
                bg='#34495e', fg='white').pack(pady=(10,5))
        
        self.topic_listbox = tk.Listbox(left_frame, height=20, font=('Arial', 11),
                                       selectmode='single', bg='#ecf0f1', fg='#2c3e50')
        self.topic_listbox.pack(pady=5, fill='both', expand=True)
        self.topic_listbox.bind('<<ListboxSelect>>', self.on_topic_select)
        
        # Right panel - Content
        right_frame = tk.LabelFrame(main_frame, text="📖 Learning Content", 
                                   font=('Arial', 14, 'bold'), bg='#34495e', fg='white',
                                   padx=10, pady=10)
        right_frame.pack(side='right', fill='both', expand=True)
        
        # Video frame
        video_frame = tk.LabelFrame(right_frame, text="🎥 Short Video Explanation", 
                                   font=('Arial', 12, 'bold'), bg='#34495e', fg='white')
        video_frame.pack(fill='x', pady=(0,10))
        
        self.video_button = tk.Button(video_frame, text="▶️ Watch Short Video (5-10 mins)",
                                     font=('Arial', 14, 'bold'), bg='#27ae60', fg='white',
                                     height=2, command=self.play_video,
                                     state='disabled')
        self.video_button.pack(pady=15, fill='x')
        
        # Notes frame
        notes_frame = tk.LabelFrame(right_frame, text="📝 Topic Notes & Formulas", 
                                   font=('Arial', 12, 'bold'), bg='#34495e', fg='white')
        notes_frame.pack(fill='both', expand=True)
        
        # Notes text area with scrollbar
        notes_text_frame = tk.Frame(notes_frame)
        notes_text_frame.pack(fill='both', expand=True, padx=5, pady=5)
        
        self.notes_text = tk.Text(notes_text_frame, wrap='word', font=('Arial', 11),
                                 bg='#ecf0f1', fg='#2c3e50', state='disabled',
                                 height=25)
        scrollbar = tk.Scrollbar(notes_text_frame, orient='vertical', command=self.notes_text.yview)
        self.notes_text.configure(yscrollcommand=scrollbar.set)
        
        self.notes_text.pack(side='left', fill='both', expand=True)
        scrollbar.pack(side='right', fill='y')
        
        # Initialize with first subject
        self.on_subject_change()
    
    def on_subject_change(self, event=None):
        subject = self.subject_var.get()
        self.topic_listbox.delete(0, tk.END)
        for topic in self.subjects_data[subject].keys():
            self.topic_listbox.insert(tk.END, topic)
        self.reset_content()
    
    def on_topic_select(self, event=None):
        selection = self.topic_listbox.curselection()
        if selection:
            subject = self.subject_var.get()
            topic = self.topic_listbox.get(selection[0])
            self.current_video = self.subjects_data[subject][topic]["video"]
            self.current_notes = self.subjects_data[subject][topic]["notes"]
            self.video_button.config(state='normal')
    
    def play_video(self):
        if hasattr(self, 'current_video'):
            webbrowser.open(self.current_video)
            messagebox.showinfo("Video Player", "Video will open in your default browser!\n\nAfter watching, check the notes below 👇")
    
    def reset_content(self):
        self.video_button.config(state='disabled')
        self.notes_text.config(state='normal')
        self.notes_text.delete(1.0, tk.END)
        self.notes_text.config(state='disabled')
    
    def get_physics_notes(self, topic):
        notes = {
            "Electrostatics": """🔬 ELECTROSTATIC PART 1 - IMPORTANT NOTES

⚡ COULOMB'S LAW:
- F = k * (q₁q₂/r²) where k = 9×10⁹ N-m²/C²
- Force is along line joining charges
- In vector form: F₁₂ = k(q₁q₂/r²) * r̂₁₂

📐 ELECTRIC FIELD:
- E = F/q = kQ/r² (r̂ direction)
- Field due to dipole at axial point: Eₐ = (1/(4πε₀)) * (2p/r³)
- Field due to dipole at equatorial point: Eₑ = (1/(4πε₀)) * (p/r³)

🔋 ELECTRIC POTENTIAL:
- V = kQ/r
- Potential due to dipole (axial): Vₐ = kPcosθ/r²
- Equipotential surfaces have same potential

⚡ GAUSS LAW:
- ∯E⋅dA = qₑₙ₍₀/ε₀
- Applications: Hollow sphere, solid sphere, infinite sheet

KEY FORMULAS:
1. Capacitance C = Q/V = ε₀A/d
2. Energy stored U = ½CV² = ½Q²/C
3. Series: 1/Cₑq = Σ(1/Cᵢ)
4. Parallel: Cₑq = ΣCᵢ

✅ IMPORTANT POINTS:
- Electric field inside conductor = 0
- Charge resides on surface of conductor
- Potential constant throughout conductor""",
            
            "Current Electricity": """🔌 CURRENT ELECTRICITY - IMPORTANT NOTES

💡 OHM'S LAW: V = IR (at constant temperature)

🔋 ELECTRIC CURRENT:
- I = Q/t = neAv (drift velocity)
- Resistance R = ρl/A
- Conductivity σ = 1/ρ

🔄 KIRCHHOFF'S LAWS:
- KCL: ΣI = 0 at junction
- KVL: ΣV = 0 in closed loop

🌡️ TEMPERATURE DEPENDENCE:
- α = (Rₜ - R₀)/R₀t
- Semiconductors: σ increases with temperature

🔋 CELLS:
- EMF(E) > Terminal Voltage(V)
- Internal resistance r = (E-V)/I
- Maximum power: R = r

🌡️ WHEATSTONE BRIDGE:
- Balanced: P/Q = R/S
- Meter bridge: 100 × l₁/l₂ = R/X

📊 POTENTIOMETER:
- Null point: k = E/(Il)
- Comparison of EMFs: E₁/E₂ = l₁/l₂

✅ KEY FORMULAS:
1. Power P = VI = I²R = V²/R
2. Heating effect H = I²Rt
3. Drift velocity v_d = I/(neA)

⚠️ TRICKS:
- Ammeter in series, Voltmeter in parallel
- For maximum power transfer: R_L = R_source""",
            
            "Magnetism": """🧲 MAGNETISM - IMPORTANT NOTES

🧲 MAGNETIC FIELD:
- B = μ₀H (vacuum)
- B = μH (material)
- M = magnetization = magnetic moment/volume

🔄 MOVING CHARGE:
- F = q(v×B)
- Radius r = mv/(qB)
- Time period T = 2πm/(qB)

🔧 SOLENOID:
- B = μ₀nI (long solenoid)
- n = N/l (turns per unit length)

🧲 TOROID:
- B = μ₀NI/(2πr)

📡 AMPERE'S CIRCUITAL LAW:
- ∮B⋅dl = μ₀I_enc

🧲 MOVING COIL GALVANOMETER:
- I = (k/NG)A
- θ = NBA/I

🔄 CYCLOTRON:
- f = qB/(2πm)
- Maximum KE = q²B²R²/(2m)

✅ IMPORTANT FORMULAS:
1. Force on wire F = BIl sinθ
2. Torque on loop τ = NIAB sinθ
3. Magnetic moment m = IA

⚠️ KEY POINTS:
- Biot-Savart law for current element
- Right hand thumb rule for field direction
- Earth's magnetic field: B_H = 0.3-0.6 gauss"""
        }
        return notes.get(topic, "Notes coming soon...")
    
    def get_chemistry_notes(self, topic):
        notes = {
            "Solid State": """🧪 SOLID STATE CHEMISTRY - IMPORTANT NOTES

🔬 CRYSTAL LATTICE:
- Unit cell: Smallest repeating unit
- Bravais lattice: 14 types
- Crystal systems: 7 types

📏 LATTICE PARAMETERS:
- Primitive: 1 atom/unit cell
- BCC: 2 atoms/unit cell (a√3/4)
- FCC: 4 atoms/unit cell (a√2/4)
- HCP: 6 atoms/unit cell

🔢 PACKING EFFICIENCY:
- Simple cubic: 52.4%
- BCC: 68%
- FCC/HCP: 74% (maximum)

🧲 DEFECTS:
- Point defects: Schottky, Frenkel
- Line defects: Edge, screw dislocations
- Schottky: Cation vacancy
- Frenkel: Cation interstitial

⚡ ELECTRICAL PROPERTIES:
- Metals: High conductivity
- Insulators: >10¹² Ωm
- Semiconductors: 10⁻⁶ to 10⁴ Ωm
- n-type: Donor impurities (P, As)
- p-type: Acceptor impurities (B, Al)

✅ KEY FORMULAS:
1. Density ρ = (Z × M)/(a³ × N_A)
2. Packing factor = (π/6√2) = 0.74 for FCC
3. Radius ratio: RC/Rₐ

📊 IMPORTANT:
- Coordination number: SC=6, BCC=8, FCC=12
- Diamond structure: FCC with T⁺ sites
- NaCl: FCC with octahedral voids""",
            
            "Solutions": """🧪 SOLUTIONS - IMPORTANT NOTES

💧 TYPES OF SOLUTIONS:
- Solid in liquid: Sugar water
- Gas in liquid: Soda water
- Solid in solid: Alloys

📏 CONCENTRATION TERMS:
- Molarity M = moles/L
- Molality m = moles/kg solvent
- Mole fraction x = moles component/total moles
- Mass % = (mass solute/mass solution)×100

⬆️ COLLIGATIVE PROPERTIES:
- Relative lowering VP = x₂ = n₂/(n₁+n₂)
- Elevation boiling ΔT_b = K_b × m
- Depression freezing ΔT_f = K_f × m
- Osmotic pressure π = CRT

🔬 VAN'T HOFF FACTOR:
- i = observed colligative/total particles
- Dissociation: i > 1
- Association: i < 1
- K_f = RT²/(1000 × ΔT_f × M)

✅ ABNORMAL MOLAR MASS:
- i = Normal MM/Abnormal MM
- NaCl: i = 1.85-1.90
- KCl: i = 1.75-1.85

📊 HENRY'S LAW:
- p = K_H × x
- K_H ↑ → Solubility ↓
- Applies to gases only

⚠️ IMPORTANT:
- Ideal solution: ΔH_mix = 0, ΔV_mix = 0
- Azeotrope: Constant boiling mixture
- Reverse osmosis: Solvent flow against gradient"""
        }
        return notes.get(topic, "Notes coming soon...")
    
    def get_math_notes(self, topic):
        notes = {
            "Relations & Functions": """📈 RELATIONS & FUNCTIONS - IMPORTANT NOTES

🔗 RELATION:
- R ⊆ A×B
- Types: Reflexive, Symmetric, Transitive, Equivalence

✅ EQUIVALENCE RELATION:
- R = {(a,a), (b,b), (a,b), (b,a)} on {a,b}

📊 FUNCTION:
- f: A→B, every a∈A has unique f(a)∈B
- Types: One-one (Injective), Onto (Surjective), Bijective

🔍 INVERSE FUNCTION:
- f⁻¹ exists if f is bijective
- f⁻¹(f(x)) = x, f(f⁻¹(x)) = x

📈 GRAPHICAL:
- One-one: Horizontal line test
- Onto: Range = Codomain

✅ IMPORTANT EXAMPLES:
1. f(x) = x³ (bijective ℝ→ℝ)
2. f(x) = sin x (neither)
3. f(x) = eˣ (one-one)

⚠️ TRICKS:
- To check reflexive: (a,a)∈R ∀a
- Symmetric: (a,b)∈R ⇒ (b,a)∈R
- f(x₁)=f(x₂) ⇒ x₁=x₂ (one-one)""",
            
            "Inverse Trigonometric Functions": """📐 INVERSE TRIGONOMETRIC FUNCTIONS

🔄 PRINCIPAL VALUES:
- sin⁻¹x: [-π/2, π/2]
- cos⁻¹x: [0, π]
- tan⁻¹x: (-π/2, π/2)

📐 IMPORTANT FORMULAS:
1. sin⁻¹x + cos⁻¹x = π/2
2. tan⁻¹x + cot⁻¹x = π/2
3. sin⁻¹(-x) = -sin⁻¹x

🔢 COMPOSITION:
- sin(sin⁻¹x) = x, |x|≤1
- sin⁻¹(sin x) = x, x∈[-π/2,π/2]

📈 KEY IDENTITIES:
- tan⁻¹a + tan⁻¹b = tan⁻¹((a+b)/(1-ab))
  (ab < 1)
- tan⁻¹a - tan⁻¹b = tan⁻¹((a-b)/(1+ab))
  (ab > -1)

✅ PROPERTIES:
1. sin⁻¹x = tan⁻¹(x/√(1-x²))
2. cos⁻¹x = tan⁻¹(√(1-x²)/x)
3. tan⁻¹(1/x) = π/2 - tan⁻¹x (x>0)

⚠️ RANGE VALUES:
- sin⁻¹(0) = 0, sin⁻¹(1) = π/2
- cos⁻¹(0) = π/2, cos⁻¹(-1) = π
- tan⁻¹(1) = π/4, tan⁻¹(∞) = π/2""",
            
            "Matrices": """🧮 MATRICES - IMPORTANT NOTES
