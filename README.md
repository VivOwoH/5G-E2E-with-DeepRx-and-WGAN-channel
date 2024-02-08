# E2E-with-NN-mapper-and-NN-receiver

Future work:
- Finish investigate epochs, ensure the constellation maps converge (i.e., they are final and show no more improvement even as we increase iterations) 
  - more iterations = less information loss; more epochs = allow NN to learn more
- Include encoder & decoder in the neural network, uncoded to coded system (coded bits may need to go through multiple channels) 
- Apply to hardware (need to add sychronization sequence in OFDM resource grid, and synchronization before receiver)
