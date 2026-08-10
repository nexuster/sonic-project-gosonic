# sonic-project-gosonic
fork of cheernoz's [GoSonic2D-Ultimate](https://github.com/cheernoz/GoSonic2D-Ultimate) framework

creating a sonic fangame using the gs2du framework, and remastering some of the code that goes with it, while also adding on new parts
this is mostly for fun, but also to strengthen my skills, and maybe learn from the engine

## things added:

* ### **ZoneMap** ( unfinished ):
  a **ZoneMap** is meant to be loaded by a **Zone** at the start and in-between acts
  uses a **ReferenceRect** to determine the camera limits

  #### *current glitches*:
    * level boundaries act weird in certain circumstances i have yet to figure out
    * *global_position* of level bounds is not correctly grabbed

* ### new **Zone** properties:
  * zone_maps - **Array\[String]**:  
    an **Array** of paths that lead to **PackedScenes**, preferably a **ZoneMap**
  * load_map(path: String) - void:  
    loads a ZoneMap from a path, sets _current_map_ to the result, and appends it's **CameraLimits** to an array
    
    ```gdscript
    func load_map(path: String) -> void:
    	var map: PackedScene = load(path)
    	var new_map: ZoneMap = map.instantiate()
    	
    	add_child(new_map)
    	var new_position := Vector2.ZERO
    	if current_map:
    		if current_map.next_map_marker:
    			new_position = current_map.next_map_marker.global_position
    	new_map.global_position = new_position
    	
    	var limits: CameraLimits = new_map._get_limits()
  	
    	acts.append(limits)
    	
    	current_map = new_map
    ```

