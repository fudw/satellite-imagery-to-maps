# satellite-imagery-to-maps

### *** Work in progress ***
<br/><br/>
I'm developing an automated pipeline that creates maps from satellite imagery and aerial sensor data using a Conditional GAN (Generative Adversarial Network) known as Pix2Pix. To train the network I use a public [dataset](https://www.kaggle.com/alincijov/pix2pix-maps) consisting of paired satellite images and street map representations. 

The original plan was to use a CycleGAN because it does not require paired examples for training. After some Googling, I actually found this Kaggle dataset with paired images, which should make the GAN learn more efficiently and stably. The dataset contains ~1000 examples, which aren't that many for this not-so-trivial task. Therefore, I will first attempt to train a Pix2Pix model on this dataset. Depending on the results, I might go for a CycleGAN and use unpaired data, which are more plentiful on the Internet, for training. 

The Pix2Pix model seems to produce decent results, which I will use as a base line. I will now move on to developing a second model for comparison.
<br/>
<br/>
### Change log
v1.14 Trained for further 50 epochs. Both generators have improved significantly without showing signs of mode collapse.

v1.13 Retrained from scratch using 0.0002 for both generator and discriminator LR following the original paper. For the first 25 epochs no mode collapse is observed in either generator. 

v1.12 Retraining with further reduced discriminator LR  from 0.0005 to 0.0002 from an earlier checkpoint before the mode collapse became frequent did not seem to prevent this from happening. 

v1.11 Further training yielded no noticeable improvement on either generator. While Sat->map performance is not far behind the pix2pix model, the Map->sat model frequently produces dark images based on maps with clear features. Yet the discriminator loss remains sufficiently finite, suggesting possible training failure on the discriminator.

v1.10 Trained for 20 more epochs with generator LR reduced from 0.0002 to 0.0001 and discriminator LR from 0.001 to 0.0005. No clear improvement seen in Sat->map gen while Map->sat gen seems to have experienced worse mode collapse, despite a strange uptick in discriminator loss. 

v1.09 Trained for 25 more epochs. Both generators seem to have platuaued while discriminator losses keep decreasing.

v1.08 Trained for 20 more epochs. Sat->map generator has made quite some improvements, while Map->sat generator may be experiencing a little mode collapse but in a less noticeable way.

v1.07 Implemented label smoothing and random noise for the discriminators. Trained for 20 more epochs with both generators producing okay-ish images. Generator loss is mostly constant while discriminator losses are trending downwards very slowly. There was one epoch where one discriminator loss dropped to zero but recovered quickly. No signs of any failure to converge so far.

#### 13.09.2021<br/>
v1.06 Trained CycleGAN from scratch for five epochs on the same dataset. Sat->map generator seems to have a much harder time than Map->sat generator for some reason.

v1.05 Trained for another 80 epochs with one-cycle cosine LR schedule that first quickly warms up to 0.01 and then slowly falling down to 0.0001. Increased weight of reconstruction loss relative to adversarial loss for generator to further focus on reproducing map features. Gen loss reduced from beginning of run by ~5% in the end.

v1.04 Trained for another 200 epochs with reduced LR by factor of 10. Gen loss still reducing although very slowly. Difficult to say whether image quality has been improving or not. 

v1.03 Retrained from scratch with much lower LR 0.0001. Implemented renormalisation of input from (0, 1) to (-1, 1); impleted Two Time-scale Update Rule (TTUR) with different LRs for generator and discriminator; implemented label smoothing for discriminator; added small random noise to both real and fake images before feeding into discriminator. Loss curves became much smoother and more stable for both generator and discriminator. No failure of convergence has been observed for the first 150 epochs.

v1.02 Further attemps to train while either maintaining or reducing LR to 0.001 failed to avoid failure to converge, i.e. discriminator loss drops to zero and doesn't recover while generator loss shoots up and image quality deteriorates notably. 

#### 30.08.2021<br/>
v1.01 Trained Pix2Pix model for 100 epochs with 0.01 LR from scratch. Generator loss becomes rather flat but discriminator loss keeps decreasing. Followed up with another 80 epochs without reducing LR. Gen loss surged while disc loss collasped to almost zero; visible deterioration in generated images.
