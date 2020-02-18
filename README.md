    First Attempt
    --------------------
    Targets:
    1. Baseline model - Start with model from S4 with 9122 and remove bias parameters 
        a. Dropout
        b. GAP Layer
        c. Conv Block after GAP layer.
        b. Slightly smaller Batch Size(64)
    2. Target stable accuracy for atleast 3-4 epochs in 20.
    3. Assignment done on Day One :)

    Results: (must include best train/test accuracies and total parameters)

    Total Parameters = 9064
    Epoch: 9 Test set: Average loss: 0.0210, Accuracy: 9940/10000 (99.400%)
    Epoch: 10 Test set: Average loss: 0.0193, Accuracy: 9943/10000 (99.430%)
    Epoch: 12 Test set: Average loss: 0.0198, Accuracy: 9941/10000 (99.410%)
    Epoch: 13 Test set: Average loss: 0.0197, Accuracy: 9940/10000 (99.400%)
    Epoch: 14 Test set: Average loss: 0.0186, Accuracy: 9941/10000 (99.410%)
    Epoch: 18 Test set: Average loss: 0.0190, Accuracy: 9946/10000 (99.460%)

    Analysis:
    1. For 20 epochs consistent results achieved with tweaked LR and batch size = 64
    2. Few spikes observed in alternate epochs.
    3. Used Padding in initial conv_blocks to prevent rapid image size reduction.
    4. Two options for next model:
        a. Use deeper model to achieve higher accuracy earlier.
        b. Smaller and more compact model with even lesser params. (Preferred next pass)
    5. Given that already the model is able to perform well, the idea was to push the parameters down further. (Wait for surprises!)	
    File Link:
    https://github.com/rajy4683/S5EVA4/blob/master/S5_EVA4_Attempt2_9946_9064.ipynb

    Second Attempt
    --------------------
    Targets:
    1. Reduce model parameters by removing the number of channels in 2nd Block.
    2. Target stable accuracy for atleast 3-4 epochs in 20.

    Results: (must include best train/test accuracies and total parameters)

    Total Parameters = 7288
    Epoch: 17 Test set: Average loss: 0.0199, Accuracy: 9942/10000 (99.420%)
    Epoch: 19 Test set: Average loss: 0.0189, Accuracy: 9938/10000 (99.380%)
    Epoch: 20 Test set: Average loss: 0.0205, Accuracy: 9939/10000 (99.390%)


    Analysis:
    1. Model showed some positive signs. It achieved 99.4 only once although for 3-4 runs was 
    Accuracy is close to target but only once was able to cross. 
    2. Training accuracy still lower than test accuracy so model. Few spikes still observed in alternate epochs.
    3. Used sligthly higher LR to achieve target accuracy as with LR=0.1, exact 99.4 only on 19th epoch
    4. Tried with multiple batch sizes (128, 239, 40, 32) but that didn't change the results drastically.
    5. 
    File Link:
    https://github.com/rajy4683/S5EVA4/blob/master/S5_EVA4_Attempt4_9942_7288.ipynb

    Third Attempt
    --------------------
    Targets:
    1. Achieve stable accuracy in 20 epochs.
    2. Use StepLR to manage lr in the later epochs to manage better accuracy 
    3. Perform hyperparameter search (used wandb agents...Not very sure if this is legal in TSAI :( )
    4. Samples of wandb sweeps:
        https://app.wandb.ai/rajy4683/uncategorized/sweeps/dj1e0q37?workspace=user-rajy4683


    Results: (must include best train/test accuracies and total parameters)

    Total Parameters = 7288
    Top Accuracy = 99.46
    Epoch: 10 Test set: Average loss: 0.0199, Accuracy: 9941/10000 (99.410%)
    Epoch: 13 Test set: Average loss: 0.0203, Accuracy: 9938/10000 (99.380%)
    Epoch: 16 Test set: Average loss: 0.0192, Accuracy: 9940/10000 (99.400%)
    Epoch: 17 Test set: Average loss: 0.0181, Accuracy: 9946/10000 (99.460%)
    Epoch: 18 Test set: Average loss: 0.0180, Accuracy: 9944/10000 (99.440%)
    Epoch: 19 Test set: Average loss: 0.0181, Accuracy: 9944/10000 (99.440%)
    Epoch: 20 Test set: Average loss: 0.0180, Accuracy: 9941/10000 (99.410%)

    Analysis:
    1. Model showed quite good results with 
        a. tweaked LR and momentum 
        b. lr-scheduling
    2. With LR scheduling, few observations were found:
        a. If LR was reduced every run with a large gamma(0.1), then accuracy targets were not achieved
        b. Till 10th epoch, model seemed to be happy with the default LR
        c. Reducing LR (with gamma=0.25 ) post 10th epoch gave much more consistent results.

    File Link:
    https://github.com/rajy4683/S5EVA4/blob/master/S5_EVA4_Attempt4_9946_7288_5.ipynb


    Fourth Attempt
    --------------------
    Targets:
    1. Achieve stable accuracy in 15 epochs. 
    2. Realized on the submission date that the target was actually within 15 epochs. World almost came down crashing!
    3. Also realized that none of the previous models were saved as the path for saving was defaulting to local dir which dies with colab runtime!!
    4. Ditched hyperparameter searching and shifted to manual mode.

    Results: (must include best train/test accuracies and total parameters)

    Total Parameters = 7288

    Epoch: 11 Test set: Average loss: 0.0186, Accuracy: 9940/10000 (99.400%)
    Epoch: 15 Test set: Average loss: 0.0174, Accuracy: 9940/10000 (99.400%)


    Analysis:
    1. Atleast the model gave some confidence, with few epochs achieving 99.4
    2. Used much higher LR (0.04), momentum (0.95) and scheduler gamma(0.5) to bring higher accuracy within 15 epochs 
    3. However, post 10th epoch, accuracy kept dropping. This could be attributed again to aggressive LR in the later stages.
    4. Next step was to manage the LR scheduling (a.k.a Playing God :) )
    File Link:
    https://github.com/rajy4683/S5EVA4/blob/master/S5_EVA4_Attempt4_9946_7288_6.ipynb


    Fifth Attempt:
    --------------------
    Targets:
    1. Achieve stable accuracy in 15 epochs....somehow :)
    2. Mainly focus on LR scheduling and stage at which LR was introduced.

    Results: (must include best train/test accuracies and total parameters)

    Total Parameters = 7288

    Epoch: 9 Test set: Average loss: 0.0189, Accuracy: 9941/10000 (99.410%)
    Epoch: 11 Test set: Average loss: 0.0184, Accuracy: 9944/10000 (99.440%)
    Epoch: 12 Test set: Average loss: 0.0182, Accuracy: 9942/10000 (99.420%)
    Epoch: 13 Test set: Average loss: 0.0184, Accuracy: 9943/10000 (99.430%)
    Epoch: 14 Test set: Average loss: 0.0186, Accuracy: 9942/10000 (99.420%)
    Epoch: 15 Test set: Average loss: 0.0185, Accuracy: 9941/10000 (99.410%)


    Analysis:
    1. LR management triggered at 5th epoch
    2. LR gamma used = 0.8
    3. Consistent accuracy reached for almost 6 epochs. 
    4. Most likely the model will bite the dust with small perturbations :(
    5. For next assignments, key takeways:
        1. If you feel assignment is done on day-one, re-read all instructions carefully. There is always a trap!
        2. LR management is not always a silver bullet but can be of  
        3. Smaller models are not necessarily the way to go
        4. 
    File Link:
    https://github.com/rajy4683/S5EVA4/blob/master/S5_EVA4_Attempt4_9946_7288_6F.ipynb


