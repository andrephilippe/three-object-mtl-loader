        import { OBJLoader, MTLLoader } from 'three-object-mtl-loader';
        import r2d2obj from './assets/obj3dpath/r2d2.obj';
        import r2d2mtl from './assets/obj3dpath/r2d2.mtl';

        const textureResolve = file =>
            require('../../../../../../assets/obj3dpath/' + file);

        const mtlLoader = new MTLLoader(THREE, textureResolve);
        mtlLoader.load(r2d2mtl, materials => {
            materials.preload();

            const objLoader = new OBJLoader(THREE);
            objLoader.setMaterials(materials);
            objLoader.load(
                r2d2obj,
                obj => this.scene.add(obj),
                xhr => {
                    console.log((xhr.loaded / xhr.total) * 100 + '% loaded');
                }
            );
        });
