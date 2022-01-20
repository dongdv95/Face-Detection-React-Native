# Face-Detection-React-Native

import {
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  Dimensions,
  Image,
  Alert,
} from 'react-native';
import React, {useState, useEffect, useRef} from 'react';
import {Image as RNimage} from 'react-native';
import {RNCamera} from 'react-native-camera';
import Permissions from 'react-native-permissions';
import imagePng from './img/glasses.png';
const maskUri = RNimage.resolveAssetSource(imagePng).uri;
function resolveImage() {
  return require('./img/glasses.png');
}
const height = Dimensions.get('window').height;
const width = Dimensions.get('window').width;
const Camera = props => {
  let [type, setType] = useState(RNCamera.Constants.Type.front);
  let [permission, setPermission] = useState('undetermined');
  const [img, setImg] = useState(null);
  const [box, setBox] = useState(null);
  let cameraRef = useRef(null);
  let options = {
    quality: 0.85,
    fixOrientation: true,
    forceUpOrientation: true,
  };

  // const handleCanvas = async canvas => {
  //   if (!(canvas instanceof Canvas)) {
  //     return;
  //   }

  //   const mask = new CanvasImage(canvas, height / 2, width / 2);
  //   mask.src = maskUri;

  //   const context = canvas.getContext('2d');

  //   mask.addEventListener('load', () => {
  //     context.drawImage(mask, 10, 10);
  //   });
  // };
  // const takePicture = async () => {
  //   if (cameraRef) {
  //     try {
  //       const data = await cameraRef.current.takePictureAsync(options);
  //       // props.onPicture(data);
  //       setImg(data.uri);
  //     } catch (err) {
  //       Alert.alert('Error', 'Failed to take picture: ' + (err.message || err));
  //       return;
  //     }
  //   }
  // };
  const onFaceDetected = ({faces}) => {
    if (faces[0]) {
      // console.log(faces[0]);
      setBox({
        box: {
          width: faces[0].bounds.size.width,
          height: faces[0].bounds.size.height,
          x: faces[0].bounds.origin.x,
          y: faces[0].bounds.origin.y,
          yawAngle: faces[0].yawAngle,
          rollAngle: faces[0].rollAngle,
        },
        rightEyePosition: faces[0].rightEyePosition,
        leftEyePosition: faces[0].leftEyePosition,
        rightMouthPosition: faces[0].rightMouthPosition,
        bottomMouthPosition: faces[0].bottomMouthPosition,
      });
    } else {
      setBox(null);
    }
  };
  //   console.log(box);
  return (
    <View style={styles.container}>
      <RNCamera
        ref={cameraRef}
        style={styles.preview}
        type={type}
        // faceDetectionClassifications={
        //   RNCamera.Constants.FaceDetection.Classifications.all
        // }
        faceDetectionLandmarks={RNCamera.Constants.FaceDetection.Landmarks.all}
        onFacesDetected={onFaceDetected}>
        {/* {box && <Canvas ref={handleCanvas} />} */}
        {box && (
          <>
            <Image
              source={require('./img/thung.png')}
              style={styles.glasses({
                rightEyePosition: box.rightEyePosition,
                leftEyePosition: box.leftEyePosition,
                yawAngle: box.box.yawAngle,
                rollAngle: box.box.rollAngle,
              })}
            />
            <View
              style={styles.bound({
                widthb: box.box.width,
                heightb: box.box.height,
                x: box.box.x,
                y: box.box.y,
              })}
            />
          </>
        )}
      </RNCamera>

      {/* <TouchableOpacity onPress={takePicture} style={styles.recordingButton}>
        <Icon name="camera" size={30} color="orange" />
      </TouchableOpacity> */}
    </View>
  );
};

export default Camera;

const styles = StyleSheet.create({
  container: {
    flex: 1,
    // display: 'flex',
    // flexDirection: 'column',
    backgroundColor: 'white',
  },
  preview: {
    flex: 1,
    // justifyContent: 'flex-end',
    // alignItems: 'center',
  },

  glasses: ({rightEyePosition, leftEyePosition, yawAngle, rollAngle}) => {
    let width = Math.abs(leftEyePosition.x - rightEyePosition.x) + 100;
    return {
      position: 'absolute',
      top: rightEyePosition.y - 145,
      left: rightEyePosition.x - 95,
      resizeMode: 'contain',
      width,
      // transform: [{rotateX: `${yawAngle}deg`}, {rotateY: `${-rollAngle}deg`}],
    };
  },
  bound: ({widthb, heightb, x, y}) => {
    return {
      position: 'absolute',
      top: y,
      left: x - widthb / 4,
      height: heightb,
      width: widthb,
      borderWidth: 2,
      borderColor: 'red',
      zIndex: 2000,
    };
  },
});
