# FlowStake Technology: Photo/Video Attestation Requirements

## User Interface and Experience (UI/UX)
- **Capture Interface:** Design an intuitive interface for users to easily capture photos or videos during their activities. This should include a clear, easy-to-use camera functionality within the app.
- **Guided Instructions:** Provide users with clear instructions on how to capture the required evidence. This might include tips on framing, lighting, and specific content that needs to be captured (e.g., a clear view of the user’s face, the activity environment, etc.).
- **Feedback Mechanism:** Implement a feedback mechanism that informs users if their photos or videos meet the required criteria or if they need to retake them.

## Technical Specifications
- **Resolution and Quality:** Set minimum resolution and quality standards for the photos and videos to ensure they are clear and usable for attestation purposes.
- **Format and Compression:** Determine acceptable file formats (e.g., JPEG, MP4) and implement compression algorithms that maintain quality while optimizing file size for efficient upload and storage.
- **Metadata Capture:** Ensure the app captures relevant metadata such as timestamp, GPS coordinates, and device information to accompany each photo or video for verification purposes.

## Security and Verification
- **Encryption:** Use end-to-end encryption to secure the photos and videos during upload and storage, ensuring that they cannot be tampered with.
- **Watermarking:** Implement digital watermarking to embed user-specific information within the photos or videos, making it difficult to use fraudulent media.
- **Blockchain Integration:** Store the attestation data on a distributed ledger (e.g., Hedera Hashgraph) to provide a tamper-proof record of the evidence. Each entry should include a hash of the photo or video file and its metadata.

## Data Storage and Management
- **Cloud Storage:** Utilize scalable cloud storage solutions (e.g., Firebase) to handle the large volume of media files. Ensure the storage system can handle peak loads during events.
- **IPFS Integration:** Use InterPlanetary File System (IPFS) for decentralized media storage. IPFS allows for efficient and distributed storage of media files, ensuring data is accessible and resilient.
- **Hash-Addressable Content:** Ensure all media files stored in IPFS are hash-addressable, meaning each file is referenced by its unique cryptographic hash. This guarantees data immutability and integrity, as any change in the file content will result in a different hash.
- **Retention Policies:** Define data retention policies to manage the lifecycle of the media files, including how long they will be stored and when they will be archived or deleted.
- **Access Control:** Implement strict access control measures to ensure that only authorized users can view or manage the attestation files.

## Attestation Process
- **Real-time Uploads:** Enable real-time uploading of photos and videos during the activity to provide immediate proof of participation and minimize post-activity fraud.
- **Peer Review System:** Allow for a peer review system where users can verify each other's submissions, enhancing community trust and engagement.
- **Automated Verification:** Develop algorithms to perform initial automated checks on the media files, such as verifying GPS data against the activity route or detecting signs of manipulation.

## User Notifications and Feedback
- **Upload Confirmation:** Notify users once their media files have been successfully uploaded and verified.
- **Verification Status:** Provide real-time updates on the verification status of their submissions, including any issues that need to be addressed.
- **Community Feedback:** Implement a system for users to receive feedback from peers and the platform on the quality and authenticity of their submissions.

## Compliance and Legal Considerations
- **Privacy Policies:** Ensure compliance with privacy regulations such as GDPR by clearly communicating how user data will be used, stored, and protected.
- **User Consent:** Obtain explicit consent from users for capturing and storing their media files as part of the attestation process.
- **Dispute Resolution:** Establish procedures for users to dispute verification results or raise concerns about privacy and data security.

## Integration with Other Features
- **Activity Feed:** Integrate the attested photos and videos into a social feed within the app, allowing users to share their achievements and engage with the community.
- **Smart Contracts:** Use Ethereum smart contracts to facilitate and enforce sports betting competitions, ensuring that the results based on attested activities are transparent and fair.

## IPFS for Media Storage and Hash-Addressable Content for Data Immutability
- **Decentralized Storage:** Leverage IPFS to store media files in a decentralized manner. This ensures high availability and resistance to censorship.
- **Content Hashing:** Utilize content hashing to ensure that each file can be uniquely identified and verified. The hash serves as a unique fingerprint for the file.
- **Data Integrity:** Guarantee data integrity by ensuring that any alteration in the media file changes its hash, thereby making tampering easily detectable.
- **Interoperability:** Ensure that the IPFS-stored media files can be accessed and verified across different systems and platforms, promoting interoperability and transparency.

By meeting these requirements, FlowStake technology can create a robust, secure, and user-friendly system for photo and video attestation, enhancing the credibility and engagement of the platform.

# FlowStake Technology / Distributed Olympics: Photo/Video Attestation Platform

This project is built using Expo and React Native, integrating IPFS for media storage and blockchain for data immutability.

## Directory Structure

/FlowStakeApp
  /assets
  /components
    /Camera.js
    /PhotoAttestation.js
    /VideoAttestation.js
  /screens
    /HomeScreen.js
    /CaptureScreen.js
    /ProfileScreen.js
  /utils
    /ipfs.js
    /blockchain.js
  App.js
  app.json
  package.json
  babel.config.js


## Code Structure

### `App.js`

```javascript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';
import CaptureScreen from './screens/CaptureScreen';
import ProfileScreen from './screens/ProfileScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Capture" component={CaptureScreen} />
        <Stack.Screen name="Profile" component={ProfileScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

### `Homescreen.js`

```javascript
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text>Welcome to FlowStake</Text>
      <Button
        title="Capture Activity"
        onPress={() => navigation.navigate('Capture')}
      />
      <Button
        title="Profile"
        onPress={() => navigation.navigate('Profile')}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

### `CaptureScreen.js`

```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import Camera from '../components/Camera';

export default function CaptureScreen() {
  return (
    <View style={styles.container}>
      <Text>Capture your activity</Text>
      <Camera />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

### `ProfileScreen.js`

```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function ProfileScreen() {
  return (
    <View style={styles.container}>
      <Text>Profile</Text>
      {/* Additional profile details can be added here */}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

### `Camera.js`

```javascript
import React, { useState, useRef } from 'react';
import { View, Button, StyleSheet } from 'react-native';
import { Camera } from 'expo-camera';
import * as FileSystem from 'expo-file-system';
import uploadToIPFS from '../utils/ipfs';

export default function CameraComponent() {
  const [hasPermission, setHasPermission] = useState(null);
  const cameraRef = useRef(null);

  React.useEffect(() => {
    (async () => {
      const { status } = await Camera.requestPermissionsAsync();
      setHasPermission(status === 'granted');
    })();
  }, []);

  const takePicture = async () => {
    if (cameraRef.current) {
      const photo = await cameraRef.current.takePictureAsync();
      await uploadToIPFS(photo.uri);
    }
  };

  if (hasPermission === null) {
    return <View />;
  }
  if (hasPermission === false) {
    return <Text>No access to camera</Text>;
  }
  return (
    <View style={styles.container}>
      <Camera style={styles.camera} type={Camera.Constants.Type.back} ref={cameraRef}>
        <View style={styles.buttonContainer}>
          <Button title="Take Picture" onPress={takePicture} />
        </View>
      </Camera>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  camera: {
    flex: 1,
  },
  buttonContainer: {
    flex: 1,
    backgroundColor: 'transparent',
    flexDirection: 'row',
    margin: 20,
  },
});
```

### `ipfs.js`

```javascript
import * as IPFS from 'ipfs-core';

const ipfs = await IPFS.create();

const uploadToIPFS = async (fileUri) => {
  try {
    const file = await FileSystem.readAsStringAsync(fileUri, {
      encoding: FileSystem.EncodingType.Base64,
    });

    const { cid } = await ipfs.add(Buffer.from(file, 'base64'));
    console.log('File uploaded to IPFS with CID:', cid);
    return cid;
  } catch (error) {
    console.error('Error uploading to IPFS:', error);
  }
};

export default uploadToIPFS;
```

### `blockchain.js`

```javascript
import Web3 from 'web3';

const web3 = new Web3('https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID');

const smartContractAddress = 'YOUR_SMART_CONTRACT_ADDRESS';
const smartContractABI = [
  // Your smart contract ABI
];

const contract = new web3.eth.Contract(smartContractABI, smartContractAddress);

export const addProofToBlockchain = async (userAddress, ipfsHash) => {
  try {
    const tx = await contract.methods.addProof(userAddress, ipfsHash).send({ from: userAddress });
    console.log('Transaction successful:', tx);
    return tx;
  } catch (error) {
    console.error('Error adding proof to blockchain:', error);
  }
};
```

### `package.json`

```javascript
{
  "name": "FlowStakeApp",
  "version": "1.0.0",
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "expo": "^46.0.0",
    "expo-camera": "^12.2.0",
    "react": "17.0.1",
    "react-dom": "17.0.1",
    "react-native": "0.64.2",
    "react-native-web": "0.17.1",
    "react-navigation": "^4.4.4",
    "react-navigation-stack": "^2.10.4",
    "ipfs-core": "^0.12.1",
    "web3": "^1.5.2"
  },
  "devDependencies": {
    "@babel/core": "^7.9.0"
  },
  "private": true
}
```

### `babel.config.js`

```javascript
module.exports = function(api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
  };
};
```

### `app.json`

```javascript
{
  "expo": {
    "name": "FlowStakeApp",
    "slug": "flowstakeapp",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": [
      "**/*"
    ],
    "ios": {
      "supportsTablet": true
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      }
    },
    "web": {
      "favicon": "./assets/favicon.png"
    }
  }
}
```

FIN
