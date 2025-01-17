## SYSTEM REQS:
- 32GB RAM (Probably more) and a GPU. 
    - Attempting to train a model on a CPU such as an Intel i7 with only 16GB RAM will absolutely crush your machine and OOM-Reaper will kill the training process.
- See the [project readme](README.md) for more details.

<hr>
<br>

## DATA PRE-PROCESSING: 
- For each task, add data to the ```./datasets``` directory. The images from two domains are placed inside  folders 'trainA/' and 'trainB/' (which you'll create). 
    - Each image file (if using unaligned triplets) consists of horizontally concatenated images, '{t, t+1, t+2}' frames from the video. The test images are placed in 'testA/' and 'testB/'. 
    - "Since we do not use temporal information at test time, the test data consists of single image '{t}'."[0] 
- See [options/train_options.py](options/train_options.py) for info on other input formats

<hr>
<br>

## TRAINING A MODEL:
NOTE: The training script expects that ```visdom```(or some other viz tool) is running on port 8097(or whatever you've configured). If there's nothing listening on the configured port, you'll see non-fatal errors written to stderr.
<br><br>
To start visdom (After installing requirements.txt):
``` bash 
visdom
# The visdom command is equivalent to running python -m visdom.server (https://pypi.org/project/visdom/#setup)
```

<br>

OTHER NOTE: To deal with truncated images, the following lines were added to `data/unaligned_triplet_dataset.py`:
``` python
from PIL import ImageFile
ImageFile.LOAD_TRUNCATED_IMAGES = True
```

TO TRAIN:
<br>
[scripts/run_Recycle_gan.sh](scripts/run_Recycle_gan.sh) contains an example of how to use the training script ```train.py```. For more info on that script's potential arguments, see [options/train_options.py](options/train_options.py). 

<br>

The training will save a model every 10 epochs(based on settings in aforementioned .sh script). You'll need to stop training manually. The models will be saved to ```.pth``` files in ```./checkpoints/<EXPERIMENT_NAME>```

<br>

You can see the loss over time by checking the `visdom` server. The [project readme](README.md) mentions some hints in terms of number of epochs required for a given amount of data.

<hr>
<br>

## Testing a model:
``` 
todo
```

<hr>
<br>

## Using a model:

``` 
todo
```

<hr>
<br>

## Other 
``` bash
# Install dependencies only for current user
# pip3 install -r requirements.txt --user

# You can use tmux so that your session will live even if disconnected (but not if you log out)
# To create a new window in the current session, press Ctrl+B, and then C. 

# To hop between windows, press Ctrl+B, and then one of the followings keys:
#     N: Display the next window.
#     P: Display the previous window.
#     0 to 9: Display a window numbered 0 to 9.
# You can also choose a window from a list. If you press Ctrl+B, and then W, a list of windows appears.

# Detaching Sessions
# If you press Ctrl+B, and then D, you will detach the session. It will continue to run in the background, but you won’t be able to see or interact with it.

# Attaching Sessions
# tmux attach-session -t geek-1

# To jump to scroll mode in an attached tmux session
# Ctrl+b, [
# (press q to quit scroll mode)

# To copy file to remote machine
# scp <FILE> -P <PORT> <USER_NAME>@<IP>:~/<FILE>
```
