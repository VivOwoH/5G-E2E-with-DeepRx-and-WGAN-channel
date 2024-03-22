# E2E-with-NN-mapper-and-NN-receiver

Future work:
- compare uncoded BLER for evaluation
- Investigate encoding scheme (currently LDPC); Define bits and channel use 
  - Repeated coding or space coding; sending same bits two times does not utilize the degree of freedom, channel 1 to channel 2 can have a phase change (e.g., 1+j, 1-j)
- DeepRx paper should have a scheme to allow lower modulation encoding to be extended to higher modulation, by selecting constellation and normalize the power to shorten the euclidean distance
- Add MLP (essentially more layers in the encoder part)
- Apply to hardware (need to add sychronization sequence in OFDM resource grid, and synchronization before receiver)
- Hardware (GNU radio) has an OFDM module already with synchronization, can plug in the autoencoder into it so that we have a demo
  - Need to check performance: how different is the channel condition
    - measure channel characteristics?
    - run training on hardware itself so we do not care about the channel?