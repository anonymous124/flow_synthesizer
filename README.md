# Generative variational timbre spaces

This repository hosts code for reproducing experiments and additional material and results for "Universal audio synthesizer control with normalizing flows" submitted at DaFX 2019.

For a better viewing experience of these additional results, please **visit the corresponding [supporting website]**.

It directly embeds the following:
  * Supplementary figures
  * Animations of descriptor space traversal (topology)
  * Audio examples of synthesized paths in the space
  * Further detailed space for perceptual inference
  * Additional data and experiments
  
You can also directly parse through the different sub-directories of the main [`docs`] directory.

## Code

### Dependencies

Code has been developed on Python3.5. It should work with other versions of Python3, but has not been tested. Moreover, we rely on several third-party libraries, listed in [`requirements.txt`]. They can be installed with `pip install -r requirements.txt`. (TODO)

The code can also work on GPUs, in which case you need to add the following dependencies (based on the premises that you have a working GPU with CUDA installed) (TODO)

### Usage

The code is mostly divided into two scripts `dafx2018learn.py` and `dafx2018figures.py`. The first script `dafx2018learn.py` allows to train a model from scratch as described in the paper. This model can be regularized or not on the timbre space. The second script `dafx2018figures.py` allows to generate the figures of the papers, and also all the supporting additional materials visible on the [supporting page](https://acids-ircam.github.io/variational-timbre/ "DaFX 2018 - Latent spaces") of this repository.

#### dafx2018learn.py arguments
```
Data-related arguments
  --filter	     Filters the data above a given octave (default : 5)
  --frames           Indexes of fromes taken in each audio file (default : from 10 to 25) 
Model-related arguments
  --name	     Name of the model
  --conditioning     Conditioning task for the model (default = 'pitch')
  --regularization   Type of regularization [prior, l2, gaussian, student]
  --mds_dims         Number of dimensions for perceptual multi-dimensional scaling
  --latent_dims      Number of latent dimensions in vae
  --hidden_dims      Dimension of hidden layers
  --hidden_layers    Number of hidden layers
  --beta             Beta weight in loss
  --alpha            Alpha weight of regularization
Properties of the learning
  --epochs           Maximum number of epochs
  --twofold_epochs   Maximum number of epochs during the regularizaion phase
# Saving
  --saveroot	     Results directory
  --save_epochs      Number of epochs between successive model saves
# Twofold learning
  --twofold          Restart learning from a previous model
  --targetdims       Which dimensions to regularize ['all', 'first', 'maxvar', 'minvar']
# GPU option
  --cuda             Index of GPU to use (-1 = CPU learning)
Monitoring
  --plot_reconstructions  Enables reconstruction plot during training
  --plot_latentspace      Enables latent space plotting during training 
  --plot_statistics       Enables latent statistics plotting during training
  --plot_npoints          Number of latent points plotted
```

#### dafx2018figures.py arguments
Import-related arguments:
  --models 		list of models imported
  --conditioning        conditioning of the models
  --filter		Filters the data above a given octave (default : 5)
  --frames		Indexes of fromes taken in each audio file (default : from 10 to 25)
GPU arguments:
  --cuda		Index of GPU to use (-1 = CPU learning)

  --descriptors_steps   Size of the descriptors grid
  --output              Figures directory

  --plot_reconstructions     Enables reconstruction plotting
  --full_instruments         Enables full instruments' sounds reconstruction
  --pairwise_paths           Enables sound sampling from an  instrument distribution to another
  --random_paths	     Enables sound sampling from random paths
  --perceptual_infer         Enables perceptual inference from test dataset
  --plot_descriptors         Enable descriptors video generation
  --descriptor_synthesis     Enables descriptor-based synthesis generation
  --labels		     In case of conditioning, labels passed for generation

#### Example runs

1. Running a l2 regularized VAE space  of musical instruments based on timbre distances

```
python3 dafx2018learn.py --regularization l2 --beta 2 --latent_dims 16 --conditioning pitch
```

2. Launching figures computation of the models embedded in the present code

```
python3 dafx2018figures.py --models trained_models/acidsInstruments-pitch-16d_full-l2_pitch-solo_3999_cpu/acidsInstruments-pitch-16d_full-l2_pitch-solo_3999_cpu.t7
```

*Important Note* : the nsgt3 package is a quick python3 adaptation of the Thomas Grill's awesome work at the address : https://github.com/grrrr/nsgt



[//]: # (LINKS)

[supporting website]: https://anonymous124.github.io/flow_synthesizer/ "DaFX 2019 - Flow synthesizer"
[`docs`]: docs/
[`requirements.txt`]: requirements.txt
