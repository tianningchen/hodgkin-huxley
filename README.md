# PSYC40/COGS21/COSC16 Computational Neuroscience
## Hodgkin-Huxley Model by T.T. Chen

The Hodgkin-Huxley Model mathematically represents neuronal actional potentials by breaking the biological process down into the 3 factors: lipid bilayer, voltage-gated time-dependent ion channels (Na+, K+, and other/"leak" channels), and induced current (by ion pumps, simulated EPSPs, etc.). These components are translated into their electrical engineering counterparts: capacitor, (variable) resistor, and current source, respectively. By knowing the current-voltage relationships for each of these electrical components, we can calculate the total change in voltage Vm across the membrane, dVm/dt. 

### Sources
I used a lot of sources here, but the most clear-cut and concise summary of the mathematics that I found was 
* **Science with Tal**'s [Hodgkin-Huxley Model of Voltage-Gated Channels Explained (Gating variables n, m, h) | Clip](https://www.youtube.com/watch?v=no_1cElnSIQ&list=PL39woqP4vGd9kP2MvRUvl81FKt6DKyshr&index=11&ab_channel=ScienceWithTal)
* **Science with Tal**'s [Python Simulation Of The Hodgkin Huxley Model | Clip](https://www.youtube.com/watch?v=qzhctJxdYyI&list=PL39woqP4vGd9kP2MvRUvl81FKt6DKyshr&index=11&ab_channel=ScienceWithTal)
* (with also, of course, some referencing to [Wikipedia article](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model) that I read to start off this project)


I also really loved watching these two lectures on the model by the professors
* **Muhammad Sabieh Anwar**: [Lecture 8: Hodgkin-Huxley model — Physics of Life (2022)](https://www.youtube.com/watch?v=WbPotJwEgBM&ab_channel=khwarizmisciencesoc)
* **Michale Fee**: ([Part 1](https://www.youtube.com/watch?v=88tKZLGOr3M&ab_channel=MITOpenCourseWare)) and ([Part 2](https://www.youtube.com/watch?v=K1pxJVdqlxw&ab_channel=MITOpenCourseWare)) of Hodgkin-Huxley Model - Intro to Neural Computation

Finally, my code is heavily based on the python youtube video by Science with Tal linked above, as well as two pre-existing projects on github! They did all the work on creating the implementation, I have just organized and edited the code based on my own intuition.
*  [Science With Tal (same link as above)](https://www.youtube.com/watch?v=qzhctJxdYyI&list=PL39woqP4vGd9kP2MvRUvl81FKt6DKyshr&index=11&ab_channel=ScienceWithTal)
    * whose code is based on [Giuseppe Bonaccorso](https://gist.github.com/giuseppebonaccorso/60ce3eb3a829b94abf64ab2b7a56aaef)
* [Scott W. HArden](https://github.com/swharden/pyHH)'s object oriented approach

### The Intuition Behind the Math

### Scratchwork & Science with Tal
Science with Tal made some beautiful diagrams illustrating the mathematical intuition behind these calculations, and here I compile the reference ones I screnshotted for myself as well as the synopsis scratchwork I made for myself.

#### My scratchwork synopsis:
![hodgkin huxley scratchwork](https://github.com/tianningchen/hodgkin-huxley/blob/main/hh_scratch.pdf)

#### Gating variables (n for potassium channel g_K; m,h for sodium channel g_Na):
![gatingvar_n intuition](https://github.com/tianningchen/hodgkin-huxley/blob/main/gatingvar_n_intuition.png)
![k current intuition](https://github.com/tianningchen/hodgkin-huxley/blob/main/k_current_intuition.png)
![na current intuition](https://github.com/tianningchen/hodgkin-huxley/blob/main/na_current_intuition.png)

#### Current equations for the potassium and sodium channels (I_K, I_Na):
![k current eqn](https://github.com/tianningchen/hodgkin-huxley/blob/main/k_current_eqn.png)
![na current eqn_m](https://github.com/tianningchen/hodgkin-huxley/blob/main/na_current_eqn_m.png)
![na current eqn_h](https://github.com/tianningchen/hodgkin-huxley/blob/main/na_current_eqn_h.png)

#### Putting current equations and membrane potential dVm/dt equation together:
![current_eqns](https://github.com/tianningchen/hodgkin-huxley/blob/main/current_eqns.png)
![dvdt_eqns](https://github.com/tianningchen/hodgkin-huxley/blob/main/dvdt_eqns.png)

