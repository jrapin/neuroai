# neuralset

A Python toolkit for building neuroimaging data pipelines — from raw data
to AI-ready batched tensors.

- **Event-driven processing** with typed, validated DataFrames
- **Multi-modal extractors** for MEG, EEG, fMRI, EMG, iEEG, text, image, audio, video
- **Caching and remote compute** via [exca](https://github.com/facebookresearch/exca)

## Install

```bash
pip install neuralset
```

## Quick example

```python
import neuralset as ns

# Load a study and download its data (MNE sample, ~1.6GB on first run).
study = ns.Study(name="Mne2013Sample", path=ns.CACHE_FOLDER)
study.download()
events = study.run()

# Configure extractors
meg = ns.extractors.MegExtractor(frequency=100.0, filter=(0.5, 30))

# Segment around triggers and build a dataset
segmenter = ns.Segmenter(
    extractors=dict(meg=meg),
    trigger_query='type == "Stimulus"',
    start=-0.1, duration=0.5,
)
dataset = segmenter.apply(events)
batch = dataset.load_all()
```

## Citation

```bibtex
@misc{king2026neuralset,
  title  = {NeuralSet: A High-Performing Python Package for Neuro-AI},
  author = {King, Jean-R{\'e}mi and Bel, Corentin and Evanson, Linnea
            and Gadonneix, Julien and Houhamdi, Sophia and L{\'e}vy, Jarod
            and Raugel, Josephine and Santos Revilla, Andrea
            and Zhang, Mingfang and Bonnaire, Julie and Caucheteux, Charlotte
            and D{\'e}fossez, Alexandre and Desbordes, Th{\'e}o
            and Diego-Sim{\'o}n, Pablo and Khanna, Shubh and Millet, Juliette
            and Orhan, Pierre and Panchavati, Saarang and Ratouchniak, Antoine
            and Thual, Alexis and Brooks, Teon L. and Begany, Katelyn
            and Benchetrit, Yohann and Careil, Marl{\`e}ne and Banville, Hubert
            and d'Ascoli, St{\'e}phane and Dahan, Simon and Rapin, J{\'e}r{\'e}my},
  year   = {2026},
  url    = {https://kingjr.github.io/files/neuralset.pdf},
  note   = {Preprint; URL will be updated when the paper lands on arXiv}
}
```

## Third-Party Content

References to third-party content from other locations are subject to
their own licenses and you may have other legal obligations or
restrictions that govern your use of that content.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
