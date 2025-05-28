<p>
  <h3 align="center">FloodMapper - Generative Floodzone Mapping Agent</h3>
<p align="center">
  <a >
    <img src="images/flood animation.gif" alt="Logo", width="250">
  </a>
</p>

This is the official repo of FloodMapper (FM), a flood mapping AI developed by @Iceofsky at the National University of Singapore. The model is based on a Generative Adversarial Network (GAN) architecture, specifically a pix2pix model, and is trained to learn from expert flood maps and extend the flood maps to unmapped regions.

## Running FloodMapper 
### 1. Install prerequisites

Use `environment.yml` to create a conda environment for FM

  ```sh
  conda env create -f environment.yml
  conda activate fm
  ```

### 2. Download weights and sample datasets
The weights files are available on figshare in the Checkpoints folder.

[DOI Link](https://doi.org/10.6084/m9.figshare.29163797)

Place the `checkpoints` and `datasets` folder in the repo.

### 3. Inference
Predictions can be carried out by running the following code where `--name` is the name of the model and `--dataroot` is the path to the directory containing the input DEM files in XYZ directory convention.

 ```sh
 python test.py --name <modelname> --dataroot <path to XYZ tile dir>
  ```

Testing an area in Texas using the TX30 model (Trained only with data in Texas):
 ```sh
python test.py --name TX30 --dataroot ./datasets/TX30/04Test/DEM
  ```

Testing an area in Texas using the USA model (Trained with data from all over the USA):
 ```sh
python test.py --name USA --dataroot ./datasets/TX30/04Test/DEM
  ```

The generated flood maps on top the DEM images will be produced in XYZ directories in `./datasets/TX30/04Test/FAKE`

### 4. Merging tiles

To merge the generated tiles into a single image, you can use the `03 postprocessing - merging of tiles.py` notebook. This script will combine all the tiles in a specified directory into a single GeoTiff image.

### 5. Train your model (optional)

For custom training, use the notebook `01 preprocessing - dataset preparation.ipynb` to prepare your own dataset. The sample dataset in datasets/TX30/03Train/TX30 is already prepared for training. 

Train the model using the sample training data in Texas, calling the model name 'TX30' (Texas 30m resolution):

 ```sh
python train.py --name TX30 --dataroot datasets/TX30/03Train/TX30 --no_instance --batchSize 6
  ```

Use `02 postprocessing - model validation.ipynb` to validate the model after training.

## Results Analysis 
For the final data, reproduction of results, and visualization used in the publication, check out this repo: [national-flood-analysis](https://github.com/Iceofsky/national-flood-analysis)


## License

Distributed under the MIT License. See `LICENSE` for more information.

## Citation

Abraham Wu, Ye Zhang, & Rudi Stouffs. Resolving the accuracy-scale-cost trilemma: Bridging inequitable access to flood information with AI generated flood maps, 06 May 2025, PREPRINT (Version 1) available at Research Square [https://doi.org/10.21203/rs.3.rs-6460834/v1]

## Contact

Contact me for collabs and ideas!

[Abraham Noah Wu](https://www.linkedin.com/in/abraham-wu-43a088b4/),  National University of Singapore, Singapore

## Acknowledgements

We gratefully acknowledge the sources of the used input data.

FloodMapper is made possible by using the following packages

* [PyTorch](https://pytorch.org/)
* [GeoPandas](https://geopandas.org/)
* [pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) - 
model architecture is heavily borrowed from the awesome repo by [junyanz](https://github.com/junyanz)
* [GANmapper](https://github.com/ualsg/GANmapper/) - 
util scripts and training configs are borrowed from the repo by [iceofsky](https://github.com/iceofsky)

