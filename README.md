# GANs_Experiments
Playing with GANs
This repo consist of an Assignment given in Deep Learning course.
The purpose of the assigment is to create two types of generative architectures:

A) GAN

b) General generative model

We implemented a GAN model in order to analyze tabular data,
The files provided for the assignment are:

• Adult.arff

• Bank-full.arff

# Pre – Processing:
In order to analyze those datasets, we made a number of adjustments – we represented the categorical 
features as numeric features using Pandas’ categorical codes, and then we normalized the features 
using MinMax scaler. 

The Adult dataset included ‘fnlwgt’ feature that represents a “final weight”, thus storing the number of 
rows that had exactly the same value. We estimated this feature is unimportant, so we chose to ignore 
it.

The relevant functions are:

• pre_process_adult

• pre_process_bank

# Convergences criteria:

In order to assess whether the generator and the discriminator have converged we defined a set of 
conditions:

First, the discriminator has to be accurate. To evaluate this condition we examined the discriminator 
performance on the validation set.
Second, both losses of the GAN modules (generator & discriminator) should be low and balanced. To 
evaluate this condition we examined the generator loss and discriminator loss by evaluating the 
validation set after each epoch.

Third, the generator needs to be strong enough to fool the discriminator (which is accurate according 
to the first criteria). For the purpose of examining this condition, we generated 1000 samples using the 
generator, and then we passed the generated samples through the discriminator. If the generator 
deceived the discriminator on enough samples we defined the generator as a good one.
The convergence criteria was defined as the combination of all of the above criteria, while the 
discriminator accuracy had to be more than 80% and the generator deception percentage has to be 
higher than 40%.

In each epoch, if the model fit all these criteria, we saved the model weights and its statistics results:


<p align="center">
<img width="279" alt="image" src="https://github.com/Habler-code/GANs_Experiments/assets/69906239/4c3394cc-d6fd-4435-9ab1-991857486d69">
</p>



As we can see from the graphs above, in both cases the discriminator loss starts with higher values than 
the generator, and after a few dozen iterations both of loss values start to act the same way and 
converge on each other. Over time, the generator gets better at tricking the discriminator (thus the 
generator loss decreases and the discriminator loss increases)

Despite the fact that the models go back and forth with their losses, it can be seen that the discriminator 
loss (colored blue) has higher loss values through the majority of the process, which indicates that the 
generator had successfully tricked it.

# Generated samples analysis:

In order to assess the Generator performance, we performed an experiment in which the generator 
produced 100 samples and then we calculated the cosine distance between the samples that fooled the 
detector and those that did not.
Using the cosine distance between the generated samples and randomly chosen samples from the 
original data, we received the following results:

**Adult dataset:**

Mean distance for samples that fooled D: 0.6314692173472443

Mean distance for samples that could not fool D: 0.823415428977838

**Bank-full dataset:**

Mean distance for samples that fooled D: 0.726186494004039

Mean distance for samples that could not fool D: 0.9328845478215896
