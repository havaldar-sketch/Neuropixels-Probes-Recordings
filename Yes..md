![][image1]![][image2]![][image3]

Refer to the three images above for Neuropixels probe recording. Refer to the following sentences/ description.  
This concept is applied for base calling and software to interpret data peaks and assign quality scores. Visual analysis involves reviewing chromatograms or signal plots to assess read accuracy, where distinct, well-separated peaks indicate high-quality data and mixed or low signals signify errors.  
Now, imagine if there is a "golden dataset/ call set of sorts". For Neuropixels probe recordings, different behavioral paradigms could be traced back to "golden datasets". And, visual analysis via image superimposition models could be built off of that (for example, via assignment of scores). Yay.

That is a fascinating bridge between genomic sequencing principles and high-density electrophysiology\! You’re essentially proposing a **"Neurometric Quality Score"** system, much like the Phred quality scores used in DNA sequencing.

In your analogy, the **"base calling"** would be the **spike sorting** process—identifying which neuron a signal belongs to. By establishing a "golden dataset," we can create a standardized ground truth to evaluate how well our algorithms (and our probes) are actually performing.

### **Translating Genomics to Neuropixels**

| Genomic Concept | Neuropixels Equivalent |
| :---- | :---- |
| **Chromatogram Peak** | **Action Potential Waveform** (the peaks/troughs in your images) |
| **Base Call** | **Spike Assignment** (assigning a waveform to a specific Unit/Neuron) |
| **Phred Score ($Q$)** | **Unit Quality Metric** (e.g., Presence Ratio, ISI Violations, Signal-to-Noise Ratio) |
| **Reference Genome** | **Golden Dataset** (curated recordings with known ground-truth labels) |

---

### **The Power of "Golden Datasets" and Superimposition**

Your idea of using **image superimposition** for visual analysis is particularly sharp. In the images you provided, we see multiple waveforms (traces) overlaid.

* **High-Quality Signal (Image 1/3):** The traces are tightly clustered with a very deep, clean trough ($\\approx \-240 \\mu V$). This represents a "high quality score" because the signal is distinct from the noise.  
* **Low-Quality/Noisy Signal (Image 2):** Notice the "fuzziness" and lower amplitude ($\\approx \-35 \\mu V$). An image superimposition model would flag this as having high variance, potentially lowering its "assignment score."

### **Implementing Your Vision**

To build the "image superimposition model" you described, the workflow would likely look like this:

1. **Template Matching:** Take the "golden" waveform from your reference dataset.  
2. **Visual Superimposition:** Layer the live recording waveform over the golden template.  
3. **Residual Analysis:** Calculate the "visual distance" between the two. If the live signal deviates significantly from the golden morphology, the software assigns a low quality score.  
4. **Behavioral Correlation:** By tracing these back to behavioral paradigms, you could identify "neural signatures" of specific actions (e.g., a reach-to-grasp task) and score how reliably those signatures are captured across different experimental sessions.

### **Why this matters**

Current spike sorting often relies on complex mathematical clustering that can be a "black box." Your approach adds a layer of **intuitive visual validation**. If the superimposed images don't look like the "golden" standard, a researcher can immediately identify data degradation or electrode drift without needing to dive into raw code.

Do you see this "golden dataset" being specific to certain brain regions (like the motor cortex), or a universal standard for probe performance?

Yes I see this being applied for different regions of the brain. Yes, we could use this as a universal standard for probe performance considering different kinds of probes (for example, chronic versus acute). 

Expanding this to a **universal standard** for probe performance could significantly bridge the gap between hardware engineering and neuroscientific data quality. By establishing these "golden datasets," you create a benchmark that accounts for the physical and temporal variables inherent in different recording environments.

### **Performance Benchmarking: Chronic vs. Acute**

Applying a "Neurometric Quality Score" allows for a direct comparison of probe stability across different experimental setups:

* **Acute Recordings:** In these "one-and-done" sessions, your visual superimposition model could flag immediate issues like **tissue dimpling** or **micro-vascular damage** if the live waveforms fail to meet the "golden" amplitude standards seen in **image\_8248e2.png**.  
* **Chronic Recordings:** Here, the model becomes a tool for longitudinal tracking. You could score the "morphological drift" of a waveform over weeks. A steady decrease in the assignment score (moving from the sharp profile of **image\_82440b.png** toward the noisier profile of **image\_824446.png**) would provide a quantitative metric for **gliosis** or probe insulation failure.

### **Regional "Golden Sets"**

Since different brain regions have distinct neuronal morphologies (e.g., the giant Pyramidal cells of the motor cortex vs. the smaller interneurons of the striatum), your model would likely need a library of region-specific templates:

| Brain Region | Waveform Characteristic | Metric Focus |
| :---- | :---- | :---- |
| **Hippocampus (CA1)** | Complex spike bursts | Inter-spike interval (ISI) consistency |
| **Motor Cortex** | High-amplitude extracellular peaks | Peak-to-trough ratio (as seen in **image\_8248e2.png**) |
| **Striatum** | Narrower, fast-spiking profiles | Waveform width and symmetry |

### **The "Software Interpreter" Advantage**

By treating Neuropixels data like genomic base calls, you move away from subjective manual curation ("This looks like a good unit") to an automated, reproducible system.

* **Visual Analysis:** Much like a chromatogram, if the superimposition shows "mixed signals" (waveforms that don't align with any known golden template), the software assigns a "low-confidence call."  
* **Universal Compatibility:** This framework could theoretically evaluate not just Neuropixels, but also **Micro-LED probes** or **flexible polymer electrodes**, scoring them against the same biological "ground truth."

This approach essentially creates a "Biological Datasheet" for every recording session, ensuring that whether a researcher is in a lab in Seattle or Zurich, a "Score of 90" represents the same level of physiological accuracy.

What would you consider the biggest hurdle in getting the community to agree on what constitutes a "Golden Dataset"—is it the diversity of the animals used, or the variability in surgical techniques?

Yes, consistency in recordings via Neuropixel probes during a session is a strong indicator of high-quality data, as it usually signifies a stable interface between the probe and the brain tissue, minimizing electrode drift and noise. However, consistency alone is not the only metric for quality. High-quality data is defined by a combination of stability, high signal-to-noise ratio (SNR), and high neuron yield. 

You've hit on the critical "Triple Threat" of electrophysiology quality control. While consistency—as visualized by the tight alignment in **image\_8248e2.png** and **image\_82440b.png**—is a prerequisite, it must be validated by the other two pillars to ensure the data is scientifically actionable.

Building your "Golden Dataset" model around these three metrics would create a robust multidimensional scoring system:

### **1\. Stability (The "Consistency" Metric)**

This measures how much the waveform morphology changes over time.

* **Visual Analysis:** Your superimposition model would look for "waveform drift." If the trough of the wave in **image\_8248e2.png** shifts horizontally or vertically across the session, it indicates the probe is moving relative to the neuron.  
* **The Score:** High stability scores mean the "base call" (the neuron identity) remains the same from the first minute to the last.

### **2\. Signal-to-Noise Ratio (SNR)**

Consistency doesn't matter if you are consistently recording noise.

* **Visual Analysis:** Compare **image\_82440b.png** with **image\_824446.png**. While they share a similar shape, the latter has significantly more "fuzz" or high-frequency jitter on the traces.  
* **The Score:** This is the equivalent of a "confidence score" in genomics. A high SNR ensures that the peaks being interpreted are actual biological events rather than electronic interference or thermal noise.

### **3\. High Neuron Yield**

In Neuropixels recordings, the density of the probe allows for hundreds of simultaneous "calls."

* **Functional Yield:** A "Golden Dataset" for a specific region (like the Hippocampus) would have a known expected density of active units.  
* **The Score:** If a probe is consistent and clean but only detects 5 neurons when the "Golden Standard" for that region is 200, the overall performance score would drop. This often points to tissue compression or "silent" zones caused by surgical trauma.

---

### **The "Golden" Multi-Index**

If we were to formalize your idea into a "Universal Standard," the assignment of scores might look like this:

| Metric | Ideal Visualization | Failure State |
| :---- | :---- | :---- |
| **Stability** | Perfect overlay of 1000+ traces. | "Ghosting" or blurred averages in the superimposition. |
| **SNR** | Deep, clear troughs (as in **image\_8248e2.png**). | Shallow, jagged waveforms (as in **image\_824446.png**). |
| **Yield** | High "unit count" across the entire probe length. | "Dead zones" where no waveforms are assigned. |

By integrating these, your model wouldn't just say "this data is consistent," it would say "this data is **high-fidelity**."

Given your interest in the regulatory side of biomedical technology, do you see this kind of standardized scoring as a potential requirement for "Regulatory Grade" neurodata in clinical trials for Brain-Computer Interfaces (BCIs)?

Yes. 

Standardizing these metrics is essentially the "missing link" for moving neurotechnology from a research tool to a **regulated medical device**. In the context of Brain-Computer Interfaces (BCIs), regulatory bodies like the FDA require objective evidence that a device is performing as intended over its entire lifespan.

Applying your "Golden Dataset" scoring system could serve as the foundation for **Biomedical Regulatory Affairs** standards in several ways:

### **1\. Verification and Validation (V\&V)**

For a BCI to be cleared for clinical use, a manufacturer must prove that the "base calling" (the translation of neural spikes into computer commands) is accurate.

* **The Golden Standard:** Regulators could mandate that BCI software be tested against a standardized library of waveforms.  
* **Performance Benchmarking:** If the device's real-time visual analysis and scoring (as seen in the high-fidelity signals of **image\_8248e2.png**) drop below a specific threshold compared to the "golden set," it could trigger an automated safety alert or recalibration protocol.

### **2\. Clinical Trial Endpoints**

In clinical trials, "High Neuron Yield" isn't just a technical preference; it’s a clinical efficacy requirement.

* **Efficacy Metric:** If a participant’s BCI stops functioning, regulators need to know *why*. Was it a software failure, or did the hardware performance degrade (e.g., shifting from the clean SNR of **image\_82440b.png** to the noisy signal of **image\_824446.png**)?  
* **Standardized Reporting:** Your proposed scoring system would allow researchers to report "Signal Quality Scores" in a format that is easily auditable by regulatory agencies, similar to how ECG or EEG data is standardized today.

### **3\. Chronic Stability Standards**

For chronic implants, the "golden dataset" would be crucial for determining the **safety profile** of the probe-tissue interface.

* **Biocompatibility Tracking:** Significant deviations from the golden waveform over time can act as a proxy for the inflammatory response or glial scarring.  
* **Regulatory Clearance:** Establishing a "Universal Standard for Probe Performance" would allow companies to demonstrate that their new probe (whether chronic or acute) meets the minimum "Quality Score" established by previous gold-standard devices.

### ---

**The Path Forward**

Since you are currently engaged with **regulatory standards and technical documentation** (such as FDA eSTAR templates), this standardized scoring could be the bridge that turns raw electrophysiology into a "Regulatory Grade" diagnostic or therapeutic tool. It transforms "nice to have" data into a rigorous **Traceability Matrix** for neural signal integrity.

Do you think the primary challenge in implementing this within a regulatory framework would be the technical software interpretation, or the difficulty of defining a "universal" biological ground truth across different human patients?

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>

[image3]: <data:image/png;base64,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>