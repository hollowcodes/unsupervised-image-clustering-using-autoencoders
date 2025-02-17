## unsupervised image classification by creating k-means clusters from bottleneck-layers of an autoencoder

## | procedure:
Create bottlenecks of the CIFAR-10 dataset (only the plane, dog and truck class) and try to group them using k-means clustering.

## | autoencoder:
![architecture](readme_images/architecture.png)

# | process:
### [autoencoder/](autoencoder/):
The autoencoder was trained to reproduce images out of 3 classes from the CIFAR-10 dataset (dogs, planes and trucks).
After training, the train-dataset was passed through the model again in evaluation mode and the bottleneck layers were saved.

### [k-means-classification/](k-means-classification/):
K-means clustering was applied on the bottleneck-datapoints with K=3, since the amount of classes was fixed.

## | results:

<details>
<summary>Click to see reconstructed images</summary>

![plane_reconstruction](readme_images/plane_reconstruction.png)
![dog_reconstruction](readme_images/dog_reconstruction.png)
![truck_reconstruction](readme_images/truck_reconstruction.png)

</details>


To measure the performance of the clustering, you can calculate the entropy of each cluster. We want every cluster to show (in the perfect case) just one class, therefore the better the clustering the lower the entropy.

<p align="center"> 
<img src="readme_images/entropy.png">
</p>

### examples cluster:
<details>
<summary>Click to see the clusters</summary>

![plane_cluster](readme_images/mainly_plane_cluster.png)
![dog_cluster](readme_images/mainly_dog_cluster.png)
![truck_cluster](readme_images/mainly_truck_cluster.png)

</details>

- the first image shows a cluster with mainly planes (lower entropy)
- the second image shows a cluster with most amount of dogs (higher entropy)
- the third image shows a cluster with most amount of trucks (higher entropy)

After training different autoencoders and clustering, it seemed that images where mostly clustered by their colors and less by their objects. Therefore a "plane"-cluster shows more accurate results because the images often have a bright-blue or white background.

