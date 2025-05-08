# Point-Cloud-Apple-Detector
### **Steps Overview**

1. **Read LAZ file**
    - Loads a point cloud using `laspy` with the `Laszip` backend.
2. **Extract and normalize RGB + XYZ**
    - Collects 3D coordinates and normalizes RGB values to `[0, 1]`.
3. **HSV Filtering for Red (Apple) Color**
    - Converts RGB to HSV and filters for reddish colors with certain saturation and brightness levels.
    - Logs how many "apple-colored" points are detected.
4. **Cluster with DBSCAN**
    - Uses `Open3D`'s DBSCAN to group nearby apple-colored points.
    - Prints size of each cluster and counts noise points.
5. **Estimate Number of Apples per Cluster**
    - Uses cluster sizes and a median-based heuristic to estimate number of apples.
    - Caps large clusters to max 5 apples.
    - Prints estimated total apples.
6. **Save Apple Points to New LAS File**
    - Saves the non-noise apple points to `apple_points_filtered.las`, all colored red.
7. **Generate Bounding Boxes Around Clusters**
    - Computes oriented bounding boxes for each cluster.
    - Saves all corner points to `apple_bboxes.las` as red points.
    - Indicates how many corners were saved.
