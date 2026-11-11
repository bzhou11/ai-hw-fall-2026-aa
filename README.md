## Assignment #7.1: Attack MNIST Recognition
## Author: Bo Zhou

## Code: 
Attack_MNIST_Recognition.ipynb: contains all code for model training, attack methods implementation, recognition rate calculation, and attack success rate (ASR) evaluation. The code was constructed and run in Google Colab with a T4 GPU.   


## Results: 
- asr_vs_epsilon.png: presents recognition rate before attacks (clean accuracy) for each model and shows plots for how attack success rate (ASR) changes as epsilon increases across three models.    
- results.json: records recognition rate before attacks (clean accuracy), epsilons, and ASR for each model.   

## General notebook description: 
The notebook covers the implementation of training three models (MLP, CNN, Transformer Encoder) on the training set, calculating recognition rate before attacks on the test set, then attacking them with gradient-based adversarial methods (FGSM, I-FGSM, MI-FGSM) and measuring attack success rates.   

The performance metrics include recognition rates before attacks (clean accuracy - classification accuracy on the clean test set) and attack success rate (ASR), which is calculated by dividing the number of test images that were correctly classified before the attack and misclassified after it by the number of test images correctly classified before attacks, for all three models separately. The epsilon values tested are [0, 0.05, 0.1, 0.15, 0.2, 0.25, 0.3] with 10 iterations for the iterative attacks, step size alpha = 2.5*epsilon /10 iterations, momentum decay = 1.0 (for MI-FGSM).    


## Results Analysis & Conclusion: 
- All three models achieve relatively high recognition rates before attacks (MLP 97.2%, CNN 98.92%, Transformer Encoder 97.93%), but none of the models withstands attacks from I-FGSM or MI-FGSM since the attack success rate (ASR) reaches 99.9-100% for all three models when epsilon increases to 0.3.   

- I-FGSM and MI-FGSM consistently present higher ASR than FGSM at every epsilon (except when epsilon = 0) for all three models. I-FGSM and MI-FGSM have relatively similar performance, with the largest ASR gap being 5.1 percentage points for CNN (I-FGSM 78.17%, MI-FGSM 73.10%) when epsilon = 0.15.   

- CNN is the most robust model compared to MLP and Transformer since it has the lowest ASR at every epsilon (epsilon>0) for all attacks.   

Overall, all three models (MLP, CNN, Transformer Encoder) reach high recognition rates (97.2% - 98.92%) before attacks, but all of them are vulnerable to the implemented adversarial attacks (FGSM, I-FGSM, MI-FGSM). The iterative attacks (I-FGSM and MI-FGSM) perform consistently better than single-step FGSM by having higher ASR at every epsilon (epsilon ≠ 0) for all three models, and I-FGSM performs similarly to MI-FGSM with the largest ASR difference of 5.1 percentage points for CNN at epsilon = 0.15. CNN is considered the most robust model of the three likely due to its local convolutional structure, but it suffers a large performance drop during I-FGSM and MI-FGSM attacks (ASR >= 99% when epsilon >= 0.25). 
