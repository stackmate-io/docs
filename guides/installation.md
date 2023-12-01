# Installation

{% hint style="info" %}
If you need to make stackmate instantly available to your team's workflow without having to install anything, perhaps you should check our [Cloud](https://stackmate.io/cloud/) version. We offer a **trial of 7 days** and **no credit card** is required.
{% endhint %}

Installing stackmate is a simple, straight forward process where all you need is an `npm` client such as `npm` itself or `yarn`

### Installation as a global package through NPM

You can install stackmate through NPM by using the following command:

```
npm install -g @stackmate/stackmate
```

### Installation as a global package through Yarn

Same for yarn:

```
yarn global add @stackmate/stackmate
```

### Direct usage through NPX

We recommend that you install stackmate globally, however if you don't want to or if you just wanna give it a quick spin, feel free to run the package directly through `npx` using the following command:

```
npx @stackmate/stackmate [preview / deploy ...] <environment> [...options]
```

{% hint style="info" %}
Throughout the course of this documentation, we will assume that the package is globally available in the system and we'll be using `stackmate` as our executable
{% endhint %}
