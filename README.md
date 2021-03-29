# Caltech Honeybee
Honeybee dataset

This repo contains:
1. Two honeybee dataset: pollen-bearing bee detection dataset and cowded bee detection dataset
2. Example code to use the dataset.

## Pollen-bearing bee detection
This dataset was derived from videos that are shot from the front view of the beehive entrance with different light condition. There are two parts. The random_selection part has 594 frames which are randomly sampled from videos, and the pollen_selection part has 357 frames which contain at least one pollen-bearing bee.

This dataset uses bounding box ([left, top, right, bottom]) to detect bees and classify them as ordinary bees and pollen-bearing bees following the format below:

```
{
	"image" : 
	{
		"width" : int, 
		"height" : int, 
		"depth": int,
		"filename" : str,
		"classmap": dict,
	}, 
	"annotations" : [
		{
			"class_id" : int,
			"bbox" : [
				left,
				top,
				right,
				bottom
			], 
			"confidence": float 
		},
	], 
}
```
### Visualization
![random selection]()
A visualzation sample in random_selection part

![pollen selection]()
A visualzation sample in pollen_selection part

## Crowded bee detection
This dataset contains 10 images that are shot from the top view of the beehive frame with different light condition. There are two parts. The orighinal part contains the original full-size images. The cropped part contains the subimages cropped from the original images, where each image has less than 30 bees.

This dataset uses oriented lines ([x0,y0,x1,y1]) to detect bees, where (x0,y0) is the location of bee's head and (x1,y1) is the tail.

For the original fullsize images, we provides the conslideated line annotation from crowdsourcing annotators for all 10 images, as well as the consolidated line annotations from three expert annotators. The data format is below:

```
{
	"image" : 
	{
		"width" : int, 
		"height" : int, 
		"depth": int,
		"filename" : str,
	}, 
	"consolidated annotations" : [
		{
			"line" : [
				x0,
				y0,
				x1,
				y1
			], 
			"num_annotators": float,
			"num_flip": float,
		},
	], 
}
```
The num_annotators refers to the number of lines that are used for consolidating this result and num_filp is the number of lines whose direction were flipped when consolidating.

For the cropped subimages, we provides the raw crowdsourcing annotations and the consolidated result using the following format:
```
{
	"image" : 
	{
		"width" : int, 
		"height" : int, 
		"depth": int,
		"filename" : str,
	}, 
	"raw annotations" : [
		{
			"workerID" : str, 
			"lines": [
				[x0,y0,x1,y1],
			]
		},
	], 
	"consolidated annotations" : [
		{
			"line" : [
				x0,
				y0,
				x1,
				y1
			], 
			"num_annotators": float,
			"num_flip": float,
		},
	], 
}
```
### Visualization
![random selection]()
A visualzation sample of original image

![pollen selection]()
A visualzation sample of cropped subimage

## Usage
See the example code.
