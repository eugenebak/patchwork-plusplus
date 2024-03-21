# patchwork-plusplus
Unofficial customized repository of [Patchwork++](https://github.com/url-kaist/patchwork-plusplus) for Point cloud segmentation


## Installation

### Python
```bash
# in patchwork-plusplus directory
$ pip install . 
```

### C++
```bash
# in patchwork-plusplus directory
$ mkdir build && cd build
$ cmake ..
$ make
```

## How to apply the ground removal with Patchwork++ in your python code

1. clone this repo in your working directory
    ```shell
    $ git clone https://github.com/eugenebak/patchwork-plusplus.git
    ```

2. Install patchwork++
    ```shell
    $ cd patchwork-plusplus
    $ pip install .
    ```

3. Import `pypatchworkpp` in the code
    ```python
    patchwork_module_path = "./patchwork-plusplus/build/python_wrapper"
    sys.path.insert(0, patchwork_module_path)
    import pypatchworkpp
    import numpy as np
    ```

4. Declare patchwork++
    ```python
    PatchworkPLUSPLUS = pypatchworkpp.patchworkpp(params)
    ```

5. Ground removal

    ```python
    PatchworkPLUSPLUS.estimateGround(point_cloud_data)
    ground_segments_points = PatchworkPLUSPLUS.getNonground()
    intensity = np.zeros(len(ground_segments_points)).reshape(-1,1)
    point_cloud_data = np.hstack((ground_segments_points, intensity))
    ```

    `point_cloud_data` is a numpy array with the shape of `(N, 4)` where `N` is the number of points.

    In this example, intensity values of non-ground points are filled with zero.
