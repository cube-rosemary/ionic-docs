---
title: "ion-router"
hide_table_of_contents: true
---
import TOCInline from '@theme/TOCInline';

import Props from '@site/static/auto-generated/router/props.md';
import Events from '@site/static/auto-generated/router/events.md';
import Methods from '@site/static/auto-generated/router/methods.md';
import Parts from '@site/static/auto-generated/router/parts.md';
import CustomProps from '@site/static/auto-generated/router/custom-props.md';
import Slots from '@site/static/auto-generated/router/slots.md';

<head>
  <title>ion-router: Router Component to Coordinate URL Navigation</title>
  <meta name="description" content="ion-router is a URL coordinator for navigation outlets of ionic: ion-nav and ion-tabs. Router components handle routing inside vanilla and Stencil JavaScript." />
</head>

import EncapsulationPill from '@components/page/api/EncapsulationPill';



<h2 className="table-of-contents__title">Contents</h2>

<TOCInline
  toc={toc}
  maxHeadingLevel={2}
/>



The router is a component for handling routing inside vanilla and Stencil JavaScript projects.

:::note
 Note: This component should only be used with vanilla and Stencil JavaScript projects. See the routing guides for [Angular](../angular/navigation), [React](../react/navigation), and [Vue](../vue/navigation) for framework-specific routing solutions.
:::


Apps should have a single `ion-router` component in the codebase.
This component controls all interactions with the browser history and it aggregates updates through an event system.

`ion-router` is just a URL coordinator for the navigation outlets of ionic: `ion-nav`, `ion-tabs`, and `ion-router-outlet`.

That means the `ion-router` never touches the DOM, it does NOT show the components or emit any kind of lifecycle events, it just tells `ion-nav`, `ion-tabs`, and `ion-router-outlet` what and when to "show" based on the browser's URL.

In order to configure this relationship between components (to load/select) and URLs, `ion-router` uses a declarative syntax using JSX/HTML to define a tree of routes.

## Basic Usage

import BasicExample from '@site/static/usage/v6/router/basic/index.md';

<BasicExample />

## Interfaces

### RouterEventDetail

```typescript
interface RouterEventDetail {
  from: string | null;
  redirectedFrom: string | null;
  to: string;
}
```

### RouterCustomEvent

While not required, this interface can be used in place of the `CustomEvent` interface for stronger typing with Ionic events emitted from this component.

```typescript
interface RouterCustomEvent extends CustomEvent {
  detail: RouterEventDetail;
  target: HTMLIonRouterElement;
}
```



## Usage

```html
<ion-router>
  <ion-route component="page-tabs">
    <ion-route url="/schedule" component="tab-schedule">
      <ion-route component="page-schedule"></ion-route>
      <ion-route url="/session/:sessionId" component="page-session"></ion-route>
    </ion-route>

    <ion-route url="/speakers" component="tab-speaker">
      <ion-route component="page-speaker-list"></ion-route>
      <ion-route url="/session/:sessionId" component="page-session"></ion-route>
      <ion-route url="/:speakerId" component="page-speaker-detail"></ion-route>
    </ion-route>

    <ion-route url="/map" component="page-map"></ion-route>
    <ion-route url="/about" component="page-about"></ion-route>
  </ion-route>

  <ion-route url="/tutorial" component="page-tutorial"></ion-route>
  <ion-route url="/login" component="page-login"></ion-route>
  <ion-route url="/account" component="page-account"></ion-route>
  <ion-route url="/signup" component="page-signup"></ion-route>
  <ion-route url="/support" component="page-support"></ion-route>
</ion-router>

```


## Properties
<Props />

## Events
<Events />

## Methods
<Methods />

## CSS Shadow Parts
<Parts />

## CSS Custom Properties
<CustomProps />

## Slots
<Slots />