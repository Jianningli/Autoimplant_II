# Autoimplant_II



```
Towards the Automatization of Cranial Implant Design in Cranioplasty II 
└── MICCAI 2021 Challenge
│   └── [Website](https://autoimplant2021.grand-challenge.org/)
└── Proceedings  ([SpringerLink](https://link.springer.com/book/10.1007/978-3-030-92652-6))
│   ├── [Personalized Calvarial Reconstruction in Neurosurgery](https://link.springer.com/chapter/10.1007/978-3-030-92652-6_1)
│   ├── [test/train/val]_cleaned_start_states.json
│   ├── time_to_keypoint_fps_{FPS}.json
│   ├── time_to_obj_state_fps_{FPS}.json
│   └── clean_clip_to_contact_point.json
└── trained_weights
│   └── *.pytar
└── objects_16k  -----  YCB objects modified for PyBullet
    └── OBJECTNAME
        └── google_16k
            ├── textured.urdf  -----  URDF to load in PyBullet
            ├── textured_big.obj  -----  Object mesh
            ├── textured_big.obj.mtl  -----  Corresponding texture
            ├── textured_bigconvex.obj  -----  Simplified mesh for collision 
            │                                   (Calculated using [v-hacd])
            └── *_keypoints.json  -----  Keypoints on the object mesh
```
