# OASIS Submission - Better Striping

## Build & Run Instructions
The following instructions should get you up and running:
1. Build and run the Dockerfile via `docker build -t osu_cdme:latest -m 2GB .`
2. Run the Dockerfile via `docker run -it osu_cdme`
3. Get this directory into the container. Options include `docker cp` and `git clone`.
4. Build the source code by running `build.bat`
5. Execute layer/scan generation for the build plate by running `run_Build_Plate.bat` and for the NIST Plate by running `run_NIST.bat`
6. You can then find the output .scn file in the location specified in the respective config file.

## Scanpath Overview
This submission does some funky things with the vectors.

It adds the following functionalities:
- **Vector Lengthening**: Iterates through every vector and, if shorter than a given length, adds a jump vector onto the end such that it takes the same time as it would have if it were that full length.
- **Vector Slicing**: Iterates through every vector and, if longer than a given length, cuts the vector into subsets all with length smaller or equal to the given length.
- **Pooled Vector Reordering**: If we just did slicing, then it wouldn't change anything. It would just add a bunch of zero-length jump vectors. Pooled Vector Reordering shuffles the order of all the individual vectors among the few vectors around it such that they have a bit of time to cool.

Note that the submission only has the second and third enabled, as using all three together seems like they would cut into each others' effectiveness pretty fast. 