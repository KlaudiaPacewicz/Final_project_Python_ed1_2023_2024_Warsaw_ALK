Manual selection of samples for model training and testing (excluding samples treated with other treatments from repository 1): 

* **model training** - selection of samples with uncertain labels:
   * *responder_based_on_PFS* == 1
   * *responder_based_on_SD* ==1 
   * *nonresponder_based_on_PFS* == 0
   * *nonresponder_based_on_SD* == 0
   * *possible_responder* == 1
   * *possible_nonresponder* == 0
 
* **model testing** - selection of samples with true labels"
   * *true_responder* == 1
   * *true_nonresponder* == 0

where 1 == RESPONDER; 0 == NONRESPONDER.
