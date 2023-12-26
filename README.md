# angular-notification [![](https://circleci.com/gh/babybeet/angular-notification.svg?style=svg&logo=appveyor)](https://app.circleci.com/pipelines/github/babybeet/angular-notification?branch=main)

A singleton, global Angular service to programmatically render notifications.

## Table of contents

<!-- toc -->

- [Installation](#installation)
- [Available APIs](#available-apis)
  - [`NotificationService`](#notificationservice)
  - [`NotificationConfiguration`](#notificationconfiguration)
  - [`Theme`](#theme)
- [Example Usage](#example-usage)
  - [Code example](#code-example)
  - [Result](#result)

<!-- tocstop -->

## Installation

- `npm`
  ```
  npm i -S @babybeet/angular-notification
  ```
- `pnpm`
  ```
  pnpm i -S @babybeet/angular-notification
  ```
- `yarn`
  ```
  yarn add @babybeet/angular-notification
  ```

## Available APIs

These are the symbols that are available from this package

### `NotificationService`

A singleton Angular service to programmatically show notifications.

```ts
class NotificationService {
  /**
   * Set the default theme that will be used for all notifications created in the future.
   *
   * @param theme The new theme to be used as the default.
   */
  static setDefaultTheme(theme: Theme): void;

  /**
   * Set the default label for the close button. Default is `Close`.
   */
  static setDefaultCloseButtonLabel(label: string): void;

  /**
   * Open a notification using the provided configuration. The opened notification
   * will be closed automatically after 10 seconds by default.
   *
   * @param notificationConfiguration The notification configuration object.
   */
  open(notificationConfiguration: NotificationConfiguration);
}
```

### `NotificationConfiguration`

The configuration object for the notification to be created.

```ts
interface NotificationConfiguration {
  /**
   * The optional number of milliseconds after which the notification is closed. Default is 10 seconds.
   */
  autoCloseMs?: number;

  /**
   * The optional class name to add for this notification.
   */
  className?: string;

  /**
   * The optional label for the notification's close button. Default is `Close`.
   */
  closeButtonLabel?: string;

  /**
   * The required notification content to show. HTML is supported.
   */
  content: string;

  /**
   * The optional theme for the floating box. Default is `light`.
   */
  theme?: Theme;
}
```

### `Theme`

```ts
type Theme = 'dark' | 'light';
```

<br/>

## Example Usage

### Code example

```typescript
// Import the service into your class to start using it
import { NotificationService } from '@babybeet/angular-notification';

@Component({
  selector: 'test-component',
  template: `
    <button
      type="button"
      (click)="showNotification()">
      Click me
    </button>
  `
})
export class TestComponent {
  constructor(private readonly notificationService: NotificationService) {}

  showNotification() {
    this.notificationService.open({
      content: 'This notification is very <strong>important</strong>'
    });
  }
}
```

### Result

| Theme |                                                                                |
| ----- | ------------------------------------------------------------------------------ |
| Light | ![Example for notification with light theme](./docs/example-1-light-theme.gif) |
| Dark  | ![Example for notification with dark theme](./docs/example-2-dark-theme.gif)   |
