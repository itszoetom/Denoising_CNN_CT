# CT Medical Imaging Denoising

Comparison of two CNN denoising models for simulated CT patches:
- `DnCNN` (residual learning)
- `U-Net` (direct image prediction)

The project is fully self-contained (no external dataset download). Data is generated from a Shepp-Logan phantom with Poisson noise at three levels.

## Quick Start
1. Create/activate a Python environment (Python 3.9+ recommended).
2. Install dependencies:
```bash
pip install torch torchvision numpy pandas matplotlib scipy scikit-image jupyter
```
3. Open and run:
- `CNNs_denoising.ipynb`
4. Run all cells from top to bottom (`Restart Kernel and Run All`).

Notes:
- Device selection is automatic (`cuda` -> `mps` -> `cpu`).
- Outputs are saved into `figures/` and `results/`.

## Folder Structure
```text
CT_Medical_Imaging_Denoising/
├── CNNs_denoising.ipynb
├── README.md
├── figures/
│   ├── 01_phantom_and_noise_levels.png
│   ├── 02_noise_histograms.png
│   ├── 03_training_curves.png
│   ├── 04_psnr_vs_noise.png
│   ├── 05_visual_comparison_medium_noise.png
│   ├── 06_difference_maps.png
│   ├── 07_visual_comparison_all_noise.png
│   ├── 08_fft_comparison.png
│   ├── 09_line_profiles.png
│   └── 10_power_spectral_density.png
└── results/
    ├── noise_stats.csv
    ├── metrics_table.csv
    ├── final_summary_table.csv
    ├── model_summary.txt
    ├── dncnn_low.pth / dncnn_med.pth / dncnn_high.pth
    └── unet_low.pth / unet_med.pth / unet_high.pth
```

## Outputs and What They Mean

### Figures (`figures/`)
- `01_phantom_and_noise_levels.png`: clean phantom and Poisson noisy versions (full + ROI).
- `02_noise_histograms.png`: clean vs noisy intensity histograms for each noise level.
- `03_training_curves.png`: train/validation loss for all 6 training runs.
- `04_psnr_vs_noise.png`: PSNR trend across noise levels for DnCNN, U-Net, Gaussian, and NLM.
- `05_visual_comparison_medium_noise.png`: side-by-side denoised patch examples (medium noise).
- `06_difference_maps.png`: absolute error maps (`|denoised - ground truth|`) for DnCNN vs U-Net.
- `07_visual_comparison_all_noise.png`: one representative patch denoised across low/med/high noise.
- `08_fft_comparison.png`: Fourier log-magnitude comparison (clean, noisy, DnCNN, U-Net).
- `09_line_profiles.png`: edge line profile comparison (resolution vs smoothing behavior).
- `10_power_spectral_density.png`: radially averaged PSD for frequency-domain tradeoff analysis.

### Results Tables/Files (`results/`)
- `noise_stats.csv`: mean/std of injected noise and SNR for each noise level.
- `metrics_table.csv`: PSNR/SSIM/edge metrics for Gaussian, NLM, DnCNN, and U-Net.
- `final_summary_table.csv`: report-ready aggregate metrics by method and noise level.
- `model_summary.txt`: model parameter counts.
- `*.pth`: saved best checkpoints from training.

## Typical Workflow for Report Writing
1. Run notebook end-to-end.
2. Use `results/final_summary_table.csv` for the main quantitative table.
3. Select 2-4 figures from `figures/` (commonly 01, 04, 05, 10) for the final PDF write-up.
