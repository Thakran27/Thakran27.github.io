# Interactive PV Cell Simulator

An interactive educational web tool for understanding photovoltaic cell physics and performance through real-time visualization and parameter exploration.

**Live Demo:** [thakran27.github.io/pv-simulator](https://thakran27.github.io/pv-simulator/)

## Overview

This simulator implements the **single-diode equivalent circuit model**, the industry-standard mathematical framework for describing photovoltaic cell behavior. Users can adjust environmental conditions (temperature, irradiance) and device parameters (series/shunt resistance) to see real-time effects on:

- **V-I Curves** (Voltage-Current characteristics)
- **P-V Curves** (Power-Voltage characteristics)
- **Performance Metrics**: Voc, Isc, Vmpp, Impp, Fill Factor, Maximum Power

## Features

### Interactive Parameters
- **Irradiance (G)**: 0–1200 W/m² (solar intensity)
- **Temperature (T)**: −40 to +80°C (cell temperature)
- **Series Resistance (Rs)**: 0–5 Ω·cm² (contact, grid losses)
- **Shunt Resistance (Rsh)**: 100–100,000 Ω·cm² (leakage current)

### Quick Presets
- **Standard Silicon**: Baseline crystalline silicon cell at STC
- **Hot Day**: High temperature, reduced irradiance
- **Cloudy Conditions**: Reduced irradiance, moderate temperature
- **CdTe**: Cadmium telluride (different bandgap, temperature coefficients)

### Real-Time Visualizations
1. **V-I Curve**: Shows operating point and short-circuit current
2. **P-V Curve**: Highlights maximum power point (MPP)
3. **Performance Metrics**: Displays key electrical characteristics
4. **Circuit Diagram**: Single-diode equivalent circuit with labeled components

### Educational Content
- Tooltips explaining each parameter and its effect
- Mathematical foundation section with key equations
- Step-by-step usage guide
- Disclaimer on simulation accuracy

## How to Use

### Getting Started (2 minutes)
1. Open the simulator in your browser
2. Click **"Standard Si"** preset to set realistic silicon cell values
3. Observe the V-I and P-V curves, and performance metrics

### Explore Irradiance Effects
- Move the **Irradiance slider** from 200 to 1000 W/m²
- **Observation**: Short-circuit current (Isc) increases proportionally; voltage (Voc) increases logarithmically
- **Real-world context**: More sunlight = more current, minimal voltage change

### Investigate Temperature Effects
- Move the **Temperature slider** from 15°C to 55°C
- **Observation**: Voltage drops significantly; current increases slightly
- **Why it matters**: Solar panels are less efficient on hot days despite higher irradiance

### Study Resistance Effects
- **Increase Series Resistance (Rs)**: Observe voltage drop under high current (power loss at MPP)
- **Decrease Shunt Resistance (Rsh)**: Simulate a defective cell with leakage current
- **Real-world context**: Contact defects, grid resistance, and shunt paths reduce performance

### Compare Materials
- Click different presets (Silicon, CdTe) to see material differences
- **CdTe has**: Higher Voc, lower Isc, different temperature coefficients
- **Silicon has**: Established manufacturing, well-understood behavior

## Mathematical Model

### Single-Diode Equation
The simulator uses the single-diode model, which is the standard for PV device physics:

```
I = Iph - Io[exp((V + I×Rs)/(n×Vt)) - 1] - (V + I×Rs)/Rsh
```

**Parameters:**
- **Iph** = Photocurrent (light-generated, proportional to irradiance)
- **Io** = Reverse saturation current (exponentially dependent on temperature)
- **V** = Cell voltage
- **I** = Cell current
- **Rs** = Series resistance (contact, grid, bulk resistance)
- **Rsh** = Shunt resistance (parallel leakage path)
- **n** = Ideality factor (≈1.3 for silicon)
- **Vt** = Thermal voltage = kT/q ≈ 0.026 V at 25°C

### Key Metrics

| Metric | Symbol | Meaning |
|--------|--------|---------|
| Open-Circuit Voltage | **Voc** | Voltage at zero current (logarithmic in irradiance) |
| Short-Circuit Current | **Isc** | Current at zero voltage (linear in irradiance) |
| Maximum Power Point Voltage | **Vmpp** | Voltage at peak power output |
| Maximum Power Point Current | **Impp** | Current at peak power output |
| Maximum Power | **Pmax** | Peak power (Vmpp × Impp) |
| Fill Factor | **FF** | Pmax / (Voc × Isc) — measure of cell quality; typical 75–85% |

### Temperature Dependencies

**Photocurrent Temperature Coefficient:**
```
Iph(T) = Iph(25°C) × [1 + α × (T - 25)]
where α ≈ 0.4–0.5 mA/(cm²·K)
```

**Bandgap Temperature Dependence:**
```
Eg(T) = Eg(0K) - α×T²/(T + β)
for silicon: Eg(0) = 1.166 eV, α = 4.73×10⁻⁴ eV/K, β = 636 K
```

**Reverse Saturation Current:**
```
Io(T) = Io(25°C) × (T/25)³ × exp[q(Eg(25) - Eg(T))/(n×k×T)]
```

## Technical Implementation

### Technology Stack
- **HTML5** + **CSS3**: Responsive, accessible interface
- **JavaScript**: Single-diode model calculations, Newton-Raphson solver
- **Chart.js**: Real-time V-I and P-V curve visualization
- **Self-contained**: No build process, runs directly in browser

### Browser Support
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile)

### Performance
- Curves update in <100 ms as parameters change
- Numerical solver converges in ~10–50 iterations
- Smooth 60 FPS animations on modern devices

## Limitations & Disclaimers

This tool provides **educational simulations** based on the single-diode model. Real PV cells exhibit additional complexity:

- **Spectral effects** (not modeled): Cell response varies with light wavelength
- **Frequency dependence** (not modeled): AC effects in grid-connected systems
- **Manufacturing variations** (not modeled): Real cells have defects, inhomogeneities
- **Advanced effects** (not modeled): Impact ionization, photon recycling, tunneling

**For engineering applications**, consult:
1. Manufacturer datasheets (J-V curves, temperature coefficients)
2. PVsyst or similar professional simulation software
3. Academic references on photovoltaic device physics

## Learning Resources

### Recommended Reading
- **Green, M. A. (2015)** — *Solar Cells: Operating Principles, Technology and Systems Applications* (comprehensive PV physics)
- **Würfel, P., & Würfel, U. (2016)** — *Physics of Solar Cells* (detailed device physics)
- **Luque, A., & Hegedus, S. (Eds., 2003)** — *Handbook of Photovoltaic Science and Engineering* (industry standard)
- **Kittel, C. (2005)** — *Introduction to Solid State Physics* (semiconductor fundamentals)

### Educational Contexts
- **Undergraduate courses**: Introduction to solar energy, semiconductor physics
- **Graduate courses**: Photovoltaic device engineering, advanced materials characterization
- **Research labs**: Initial parameter exploration before detailed device simulation
- **Industry training**: Engineer onboarding, customer education

## Contributing

This project is designed for educational use. Suggestions for improvements:

1. **Additional materials**: Perovskite, CIGS, III-V compounds
2. **Advanced features**: Module-level simulation, mismatch losses, temperature profiles
3. **Accessibility**: More visualization options, export functionality
4. **Documentation**: Additional tutorials, solved problems, case studies

To contribute, please open an issue or pull request on the [GitHub repository](https://github.com/Thakran27/Thakran27.github.io).

## Citation

If you use this simulator in research or education, please cite:

```
Thakran, A. (2025). Interactive PV Cell Simulator. 
Retrieved from https://thakran27.github.io/pv-simulator/
```

For academic papers:

```bibtex
@software{thakran2025pvsim,
  author = {Thakran, Anjali},
  title = {Interactive {P}hotovoltaic {C}ell {S}imulator: {E}ducational {T}ool for {S}olar {C}ell {P}hysics},
  year = {2025},
  url = {https://thakran27.github.io/pv-simulator/},
  note = {Accessed: \today}
}
```

## License

This tool is provided as an educational resource. Feel free to use, modify, and share for educational and research purposes.

## Author

**Dr. Anjali Thakran**  
Postdoctoral Fellow, Thematic Center for Green Energy  
Research Center for Critical Issues, Academia Sinica

**Contact:** [anjalithakran83@gmail.com](mailto:anjalithakran83@gmail.com)  
**Website:** [thakran27.github.io](https://thakran27.github.io)  
**LinkedIn:** [linkedin.com/in/anjali1997](https://linkedin.com/in/anjali1997)

---

**Built with ⚡ physics · 🎓 education · 🔬 research**
