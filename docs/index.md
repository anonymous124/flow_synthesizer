<!--
<script src="http://vjs.zencdn.net/4.0/video.js"></script>
-->

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

<script type="text/javascript"> 
      // Show button
      function look(type){ 
      param=document.getElementById(type); 
      if(param.style.display == "none") param.style.display = "block"; 
      else param.style.display = "none" 
      } 
</script> 

# Universal audio synthesizer control with normalizing flows

This website presents additional material and experiments around the paper *Universal audio synthesizer control with normalizing flows*.

The ubiquity of sound synthesizers has reshaped music production and even entirely defined new music genres. However, the increasing complexity and number of parameters in modern synthesizers make them harder to master. We thus need methods to easily create and explore with synthesizers.

Our paper introduces a radically novel formulation of audio synthesizer control. We formalize it as finding an organized latent audio space that represents the capabilities of a synthesizer, while constructing an invertible mapping to the space of its parameters. By using this formulation, we show that we can address simultaneously *automatic parameter inference, *macro-control learning* and *audio-based preset exploration* within a single model. To solve this new formulation, we rely on Variational Auto-Encoders (VAE) and Normalizing Flows (NF) to organize and map the respective *auditory* and *parameter* spaces. We introduce a new type of NF named *regression flows* that allows to perform an invertible mapping between separate latent spaces, while steering the organization of some of the latent dimensions.

**Contents**
  * [Audio reconstruction](#audio-reconstruction)
  * [Macro-control learning](#macro-control-learning)
  * [Audio space interpolation](#audio-space-interpolation)
  * [Neighborhood exploration](#neighborhood-exploration)
  * [Vocal sketching](#vocal-sketching)
  * [Real-time implementation using Ableton Live](#real-time-implementation-using-ableton-live)
  * [Code](#code)


## Audio reconstruction

Below are a few examples of audio reconstructed by the models tested in the paper. The first sound is a sample drawn from the test set, and the second is its reconstruction.

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/ae_mel_mse_cnn_mlp_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/cnn_mel_mse_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/gated_cnn_mel_mse_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/gated_mlp_mel_mse_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/mlp_mel_mse_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/res_cnn_mel_mse_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_flow_mel_mse_cnn_flow_cde_iaf_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_flow_mel_mse_cnn_flow_kl_f_iaf_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_flow_mel_mse_cnn_mlp_iaf_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_flow_mel_mse_cnn_mlp_iaf_2_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_mel_mse_cnn_mlp_1_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/vae_mel_mse_cnn_mlp_2_batch_1.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/reconstruction/wae_mel_mse_cnn_mlp_1_batch_1.wav" type=audio/wav>
</audio>


## Macro-control learning

The latent dimensions can be seen as meta-parameters for the synthesizer that naturally arise from our framework. Moreover, as they act in the latent audio space, one could hope they impact audio features in a smoother way than native parameters.

The following figure presents the evolution of synth parameters and corresponding spectrogram while moving along two dimensions of the latent space. The spectrograms show a smooth variation in audio features, while parameters move in a clearly non-independent and less smooth fashion. This proves that latent dimensions rather encode audio features than simply parameters values.

<img src="figures/meta_parameters.png" align="middle">



## Audio space interpolation

In this experiment, we select two audio samples, embed them in the latent space, and continuously interpolate in between. At each interpolated latent point, we are able to output the corresponding synthesizer parameters and thus to synthesize audio.

<img src="figures/interpolation.png" align="middle">

Below are the two audio samples, drawn from the test set:

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/interpolation/p0.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/interpolation/p1.wav" type=audio/wav>
</audio>

And here are the interpolations output by the different models:

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/interpolation/p0.wav" type=audio/wav>
</audio>

<audio controls preload="auto" data-setup="{}" width="100%"> 
<source src="audio/interpolation/p1.wav" type=audio/wav>
</audio>


## Neighorhood exploration



## Vocal sketching



## Real-time implementation using Ableton Live

Not available yet.

## Code

The full code will only be released after the end of the review process and will be available on the corresponding [GitHub repository](https://github.com/anonymous124/flow_synthesizer).

