# Heart Rate API

A simple API to estimate heart rate using PPG analysis data from mobile camera.

## Use 

- Record a 15 second video by keeping finger over the camera with flash on.
- Send url link of video to the api to perform PPG and estimate heart rate.

## Approach

- Place finger over the camera and 15 second video was recorded with flash on in each case.
- This video is imported to our python based api using ```open cv2``` and video object was created, FPS, frame count were determined.
- The first few frames and last few frames were dropped as a data pre processing measure as they contain most of the error.
```eg. placing finger and removing finger, stablizing time etc.```
- For each image of the video, pixels in the middle were selected and average of RGB colors were calculated.
- Array of each RGB color was maintained to storage average values.
- Array with red pixels was selected for further processing and determination of results as red color gives best result `
(Assumption)`
- Following arrays were treated as signal objects.
- `Lowpass filter` and `highpass filter` is use to remove unwanted frequencies from signals.
- Further, signal was squared to elongate it, so that it was easy to determine peaks `(Assumption)`
- Peaks were detected using peak detection algorithm from `SCIPY.SIGNAL` library and average time between peaks were calculated.
- Thus, calculating **Heart rate**.


## Example of API response

```
API response example

{
   "avg_bpm":116.3654074742016,
   "time":06-01-2023
}
```
## References

- [**Scipy Signal**](https://docs.scipy.org/doc/scipy/reference/signal.html)
- [**Research Gate**](https://www.researchgate.net/publication/329896875_Image_Analysis_on_Fingertip_Video_To_Obtain_PPG)
- [**Open CV**](https://docs.opencv.org/3.4/d8/dfe/classcv_1_1VideoCapture.html)
- [**heart rate ppg camera**](https://www.researchgate.net/publication/329896875_Image_Analysis_on_Fingertip_Video_To_Obtain_PPG)
