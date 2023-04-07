[View code on GitHub](https://github.com/nervosnetwork/ckb/resource/src/lib.rs)

The code in this file is responsible for bundling resources in the ckb binary. The resources include ckb.toml, ckb-miner.toml, default.db-options, and all files in the directory `specs`. The bundled files can be read via `Resource::Bundled`. The code provides functions to create references to bundled resources and resources resident in the local file system. It also provides functions to create the CKB config file resource, the CKB miner config file resource, and the RocksDB options file resource from the file system. 

The code exports a bundled resource to a specified directory by combining `root_dir` and the resource identifier. The bundled files can be customized for different chains using spec branches. The code checks whether any of the bundled resources have been exported in the specified directory. 

The code defines a struct `Resource` that represents a resource, which is either bundled in the CKB binary or resident in the local file system. The struct has two variants: `Bundled` and `FileSystem`. The `Bundled` variant has an identifier of the bundled resource, while the `FileSystem` variant has a file path to the resource. The struct has methods to create references to the bundled resource and the file system resource. It also has methods to check whether the resource exists, get the resource content, and export a bundled resource. 

The code defines a struct `SourceFiles` that represents the bundled resources in the CKB binary. The struct has two fields: `system_cells` and `config`. The `system_cells` field is a reference to the bundled system cells, while the `config` field is a reference to the bundled config files. The struct has methods to get the resource content, read the resource content via an input stream, and check whether the resource is available. 

The code defines a function `from_utf8` that converts a `Cow<[u8]>` to a `String`. The function is used to convert the resource content to a string. 

The code defines a function `join_bundled_key` that joins a root directory and a key to form a path. The function is used to export a bundled resource to a specified directory.
## Questions: 
 1. What files are bundled in the binary by this crate?
   
   This crate bundles the files ckb.toml, ckb-miner.toml, default.db-options, and all files in the directory `specs` in the binary.

2. How can the bundled files be read?
   
   The bundled files can be read via `Resource::Bundled`, for example:
   
   ```
   // Read bundled ckb.toml
   use ckb_resource::{Resource, CKB_CONFIG_FILE_NAME};

   let ckb_toml_bytes = Resource::bundled(CKB_CONFIG_FILE_NAME.to_string()).get().unwrap();
   println!("ckb.toml\n{}", String::from_utf8(ckb_toml_bytes.to_vec()).unwrap());
   ```

3. How can the bundled files be customized for different chains using spec branches?
   
   These bundled files can be customized for different chains using spec branches. See [Template](struct.Template.html).