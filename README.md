# satellite-imagery-to-maps

### *** Work in progress ***
<br/><br/>
I'm developing an automated pipeline that creates maps from satellite imagery and aerial sensor data using a Conditional GAN (Generative Adversarial Network) known as Pix2Pix. To train the network I use a public [dataset](https://www.kaggle.com/alincijov/pix2pix-maps) consisting of paired satellite images and street map representations. 

The original plan was to use a CycleGAN because it does not require paired examples for training. After some Googling, I actually found this Kaggle dataset with paired images, which should make the GAN learn more efficiently and stably. The dataset contains ~1000 examples, which aren't that many for this not-so-trivial task. Therefore, I will first attempt to train a Pix2Pix model on this dataset. Depending on the results, I might go for a CycleGAN and use unpaired data, which are more plentiful on the Internet, for training. 
<br/>
<br/>
