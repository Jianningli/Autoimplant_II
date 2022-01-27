# [Autoimplant_II](https://autoimplant2021.grand-challenge.org/)

```
Towards the Automatization of Cranial Implant Design in Cranioplasty II 
└── MICCAI 2021 Challenge
└── Proceedings  
│   ├── Personalized Calvarial Reconstruction in Neurosurgery
│   ├── Qualitative Criteria for Feasible Cranial Implant Designs
│   ├── Segmentation of Defective Skulls from CT Data for Tissue Modelling
│   ├── Improving the Automatic Cranial Implant Design in Cranioplasty by Linking Different Datasets
│   ├── Learning to Rearrange Voxels in Binary Segmentation Masks for Smooth Manifold Triangulation
│   ├── A U-Net Based System for Cranial Implant Design with Pre-processing and Learned Implant Filtering
│   ├── Sparse Convolutional Neural Network for Skull Reconstruction
│   ├── Cranial Implant Prediction by Learning an Ensemble of Slice-Based Skull Completion Networks
│   ├── PCA-Skull: 3D Skull Shape Modelling Using Principal Component Analysis
│   ├── Cranial Implant Design Using V-Net Based Region of Interest Reconstruction
```

├── Proceedings: [SpringerLink](https://link.springer.com/book/10.1007/978-3-030-92652-6)     
01. [Personalized Calvarial Reconstruction in Neurosurgery](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_1).
02. [Qualitative Criteria for Feasible Cranial Implant Designs](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_2).
03. [Segmentation of Defective Skulls from CT Data for Tissue Modelling](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_3).
04. [Improving the Automatic Cranial Implant Design in Cranioplasty by Linking Different Datasets](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_4). [[**<ins>code</ins>**](https://github.com/MWod/AutoImplant_2021)].
6. [Learning to Rearrange Voxels in Binary Segmentation Masks for Smooth Manifold Triangulation](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_5). [[**<ins>code</ins>**](https://github.com/Jianningli/voxel_rearrangement)]
7. [A U-Net Based System for Cranial Implant Design with Pre-processing and Learned Implant Filtering](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_6).
8. [Sparse Convolutional Neural Network for Skull Reconstruction](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_7). [[**<ins>code</ins>**](https://github.com/akroviakov/SparseSkullCompletion)]
9. [Cranial Implant Prediction by Learning an Ensemble of Slice-Based Skull Completion Networks](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_8). [[**<ins>code</ins>**](https://github.com/YouJianFengXue/Cranial-implant-prediction-by-learning-an-ensemble-of-slice-based-skull-completion-networks)]
10. [PCA-Skull: 3D Skull Shape Modelling Using Principal Component Analysis](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_9). [[**<ins>code</ins>**](https://github.com/1eiyu/ShapePrior)]
11. [Cranial Implant Design Using V-Net Based Region of Interest Reconstruction](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_10).




├── code snippets for implant post-processing (thinning & border adjustment)

```Python
import nrrd
import pyvista as pv
import numpy as np
import vtk
import trimesh

# original mesh
mesh = pv.PolyData('original.stl')
# extract the interior surface of an implant
mesh.compute_normals(cell_normals=True, point_normals=False, inplace=True)
ids = np.arange(mesh.n_cells)[mesh['Normals'][:,2] < 0.0 ]
top = mesh.extract_cells(ids)


ind= []
newList1=[]
newList2=[]
# convert pyvista datatype to list for fast processing of points

for i  in range(len(top.points)):
	newList1.append([top.points[i][0],top.points[i][1],top.points[i][2]])


for i  in range(len(mesh.points)):
	newList2.append([mesh.points[i][0],mesh.points[i][1],mesh.points[i][2]])

for i  in range(len(top.points)):
	idx=newList2.index(newList1[i])
	ind.append(idx)

# rescale x,y,z

for  i in range(len(ind)):
	mesh.points[ind[i]][2]=mesh.points[ind[i]][2]*1.05
	mesh.points[ind[i]][1]=mesh.points[ind[i]][1]*0.95
	mesh.points[ind[i]][0]=mesh.points[ind[i]][0]*1.00


mesh.plot()
mesh=mesh.extract_surface().triangulate()
mesh.save('result.stl')

# after generating the processed mesh. Intersection can be done using ([MeshLab](https://www.meshlab.net/)):
#MeshLab - Loading result.stl and original.stl - Filters - Remeshing, Simplification, Reconstruction - Mesh Boolean: Intersection


```



