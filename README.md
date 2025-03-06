#  팬텀 월렛 SDK

이 모노레포에는 팬텀 월렛 SDK와 그 사용을 보여주는 데모 애플리케이션이 포함되어 있습니다.

##  개요

팬텀 월렛 SDK를 사용하면 팬텀의 지갑 기능을 웹 애플리케이션에 직접 통합할 수 있습니다. 지갑 UI 보여주기/숨기기, 스왑 및 구매 수행, 솔라나, 이더리움, 수이, 비트코인용 체인별 RPC 인터페이스 접속 등 지갑과 상호작용하기 위한 간단한 인터페이스를 제공한다.

##  패키지

- **@phantom/지갑-sdk**: 팬텀 지갑 통합을 제공하는 핵심 SDK.
- **@phantom/데모앱**: SDK 사용 방법을 보여주는 React 기반 데모 앱입니다.

## 시작하기

### 설치

```바쉬
npm 사용 #
NPM 설치 @phantom/지갑-SDK

원사를 사용하는 #
실 추가 @phantom/지갑-sdk

pnpm을 사용하는 #
pnpm 추가 @phantom/지갑-sdk
```

###  기본사용법

```활자
"@phantom/wallet-sdk"에서 가져오기 {Phantom, Position }를 생성합니다.

// 지갑 인스턴스 생성
const phantom = wait createPhantom({
 위치: 위치.bottomRight, 
 hideLauncherBeforeOnboarded: false, 
 네임스페이스: "my-app", 
});

// 지갑을 보여주세요
팬텀.쇼();

// 블록체인 특화 인터페이스에 액세스하십시오.
// 솔라나
const solanaPublicKey = wait phantom.solana.connect();
console.log("Connected Solana Account:", solanaPublicKey.toString());

// Ethereum
const ethereumAccounts = await phantom.ethereum.request({
  method: "eth_requestAccounts",
});
console.log("Connected Ethereum account:", ethereumAccounts[0]);

// Use wallet functions
phantom.buy({ buy: "solana:101/nativeToken:501" }); // Buy SOL
phantom.swap({
  buy: "solana:101/address:EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v",
  sell: "solana:101/nativeToken:501",
}); // Swap SOL to USDC
```

## Blockchain RPC Interfaces

The SDK provides access to Phantom's blockchain-specific RPC interfaces:

- `phantom.solana` - Solana RPC interface
- `phantom.ethereum` - Ethereum, Base, and Polygon RPC interface
- `phantom.sui` - Sui RPC interface
- `phantom.bitcoin` - Bitcoin RPC interface

## Development

```bash
# Install dependencies
yarn install

# Start the demo app
yarn start:demo

# Build all packages
yarn build
```

## Give Feedback

Phantom Embedded is in active development and will be prioritizing features requested by early adopters. If you are
interested in working with us, please email us at `developers@phantom.app` or message `@brianfriel` on Telegram.

## Frequently Asked Questions

<details>
  <summary>How does the embedded wallet work with the Phantom extension?</summary>

    If the Phantom extension is detected, we will not inject the embedded wallet. Phantom users can continue using their extension like normal.

    If you want to use the embedded wallet and the Phantom extension, you need to instantiate the wallet with a custom namespace.

</details>
<details>
  <summary>What does `createPhantom()` do?</summary>

    The Phantom embedded wallet lives inside an iframe. The `createPhantom` function loads and attaches the iframe to your website.

</details>
<details>
  <summary>How do I interact with the embedded wallet?</summary>

    Once `createPhantom` has been called, `window.phantom.solana` and a compliant wallet-standard provider will also be available in the global scope of your website. This means that most of your existing code for interacting with Solana wallets should work out of the box.

    Once a user has onboarded to the embedded wallet, they should be able to click your “connect wallet” button, which gives your website access to their Solana address. After that, signing messages and transactions should just work as normal.

    If you use a namespace, you will need to invoke the functions through the `window[namespace]` object, or directly through the returned Phantom instance.

</details>
<details>
  <summary>I can't see the embedded wallet on my website. What's wrong?</summary>

    The most common cause is that you are using a browser with the Phantom extension installed. If the Phantom extension is detected, we will not inject the embedded wallet, unless you use a custom namespace.

    You can temporarily disable the Phantom extension by going to `chrome://extensions` and toggling Phantom off.

</details>
<details>
  <summary>How much does this cost?</summary>

    It's free!

</details>

## Disclaimers

The embedded wallet is a beta version, and Phantom will not be liable for any losses or damages suffered by you or your end users.

Any suggestions, enhancement requests, recommendations, or other feedback provided by you regarding the embedded wallet will be the exclusive property of Phantom. By using this beta version and providing feedback, you agree to assign any rights in that feedback to Phantom.
