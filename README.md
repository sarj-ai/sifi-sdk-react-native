# @sifi/react-native-sdk

[![npm version](https://badge.fury.io/js/@sifi%2Freact-native-sdk.svg)](https://www.npmjs.com/package/@sifi/react-native-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official Sifi React Native SDK for seamless chat integration with runtime binary downloading.

## 📱 Current Version: v0.1.2

## Installation

```bash
npm install https://sarj-ai.github.io/sifi-sdk-react-native/releases/latest/sifi-react-native-sdk.tgz react-native-webview
```

### Alternative Installation (Specific Version)

```bash
npm install https://sarj-ai.github.io/sifi-sdk-react-native/releases/0.1.2/sifi-react-native-sdk-0.1.2.tgz react-native-webview
```

### iOS Setup

```bash
cd ios && pod install
```

### Android Setup

No additional setup required.

## Quick Start

### 1. Configure the SDK

```typescript
import { SifiSDKManager } from '@sifi/react-native-sdk';

const configureSdk = () => {
  const sdkManager = SifiSDKManager.getInstance();
  
  sdkManager.configure({
    chatUrl: 'https://chat.sifi.io/your-chat-id'
  });
  
  console.log('SDK configured!');
};
```

### 2. Use the SifiChatView Component

```typescript
import React from 'react';
import { View } from 'react-native';
import { SifiChatView } from '@sifi/react-native-sdk';

export default function ChatScreen() {
  return (
    <View style={{ flex: 1 }}>
      <SifiChatView
        style={{ flex: 1 }}
        onLoadStart={() => console.log('Chat loading...')}
        onLoadEnd={() => console.log('Chat loaded!')}
        onError={(error) => console.error('Chat error:', error)}
      />
    </View>
  );
}
```

### 3. Complete Example

```typescript
import React, { useEffect, useState } from 'react';
import { View, Text, ActivityIndicator } from 'react-native';
import { SifiSDKManager, SifiChatView } from '@sifi/react-native-sdk';

export default function App() {
  const [isReady, setIsReady] = useState(false);

  useEffect(() => {
    initializeSdk();
  }, []);

  const initializeSdk = () => {
    const sdkManager = SifiSDKManager.getInstance();
    
    sdkManager.configure({
      chatUrl: 'https://chat.sifi.io/your-chat-id'
    });
    
    setIsReady(true);
  };

  if (!isReady) {
    return (
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <ActivityIndicator size="large" />
        <Text>Initializing Sifi SDK...</Text>
      </View>
    );
  }

  return <SifiChatView style={{ flex: 1 }} />;
}
```

## API Reference

### SifiSDKManager

#### Methods

- `getInstance(): SifiSDKManager` - Get singleton instance
- `configure(config: SifiSDKConfig): void` - Configure SDK with chat URL
- `getChatUrl(): string | null` - Get configured chat URL
- `getConfig(): SifiSDKConfig | null` - Get current configuration
- `isConfigured(): boolean` - Check if SDK is configured

#### SifiSDKConfig Interface

```typescript
interface SifiSDKConfig {
  chatUrl: string;
}
```

### SifiChatView Component

#### Props

```typescript
interface SifiChatViewProps {
  style?: ViewStyle;
  onLoadStart?: () => void;
  onLoadEnd?: () => void;
  onError?: (error: any) => void;
}
```

## Requirements

- React Native >= 0.60.0
- React >= 16.8.0
- react-native-webview >= 11.0.0

## Support

- **Issues**: [GitHub Issues](https://github.com/sarj-ai/sifi-sdk-react-native/issues)
- **Documentation**: [docs.sifi.io](https://docs.sifi.io)
- **Support**: support@sifi.io

## License

MIT © Sifi

---

**Latest Release**: v0.1.2 - Initial release with runtime binary downloading  
**Release Date**: 2025-07-14
