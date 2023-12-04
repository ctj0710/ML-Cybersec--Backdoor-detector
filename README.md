# ML-Cybersec--Backdoor-detector

## Repository Structure

- `Repaired_models`
    - `model_X=2.h5` // Model pruned with 2% accuracy drop
    - `model_X=4.h5` // Model pruned with 4% accuracy drop 
    - `model_X=10.h5` // Model pruned with 10% accuracy drop 

- `ct3002-lab4.ipynb` // ipynb code with execution
- `ct3002_Lab4_report.pdf`
- `eval.py` // Evaluation script


## Dependencies
- Python 
- Keras 
- Numpy 
- Matplotlib 
- H5py 
- TensorFlow-gpu 

## Data
Download the validation and test datasets from [here](https://github.com/csaw-hackml/CSAW-HackML-2020/tree/master) and under lab3/ directory.

- `lab3`
  - `data`
    - `cl`
      - `valid.h5` // clean validation data used to design the defense
      - `test.h5` // clean test data used to evaluate the BadNet
    - `bd`
      - `bd_valid.h5` // sunglasses poisoned validation data
      - `bd_test.h5` // sunglasses poisoned test data
  - `models`
    - `bd_net.h5` // badnet model used in Lab3
    - `bd_weights.h5` // badnet model weights


The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets. `bd_valid.h5` and `bd_test.h5` contain validation and test images with a sunglasses trigger respectively, activating the backdoor for `bd_net.h5`.


## Submission

The concept involves pruning the `conv_3` layer based on the last pooling average activation across the entire validation dataset. Models are saved when accuracy drops by 2%, 4%, and 10%, labeled as `model_X=2.h5`, `model_X=4.h5`, and `model_X=10.h5`, respectively. To create a goodNet, the BadNet and the repaired model are combined, and the program is found in the `ct3002_lab4.ipynb` file.


- To run the `eval.py` script:

```bash
python eval.py <test data directory> <repaired model directory>
```
For Example:
```bash
python eval.py /kaggle/input/mlcybersec/lab3/data/cl/test.h5  /kaggle/input/mlcybersec/lab3/model/bd_net.h5 Repaired_models/model_X=10.h5
