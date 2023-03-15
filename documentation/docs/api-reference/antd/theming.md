---
id: theming
title: Theme
sidebar_label: Theme 🆙
---

Ant Design allows you to customize design tokens to satisfy UI diversity from business or brand requirements, including primary color, border radius, border color, etc.
Design Tokens are the smallest element that affects the theme. By modifying the Design Token, we can present various themes or components.

[Refer to the Ant Design documentation for more information about customizing Ant Design theme. &#8594](https://ant.design/docs/react/customize-theme)

## Theme customization

[`<ConfigProvider/>`](https://ant.design/components/config-provider/#components-config-provider-demo-theme) component can be used to change theme. It is not required if you decide to use the default theme.

### Overriding the themes

You can override or extend the default themes. You can also create your own theme. Let's see how to do this.

```tsx
import { Refine } from "@refinedev/core";
import { Layout, ConfigProvider } from "@refinedev/antd";

const API_URL = "https://api.fake-rest.refine.dev";

const App: React.FC = () => {
    return (
        // highlight-start
        <ConfigProvider
            theme={{
                components: {
                    Button: {
                        borderRadius: 0,
                    },
                    Typography: {
                        colorTextHeading: "#1890ff",
                    },
                },
                token: {
                    colorPrimary: "#f0f",
                },
            }}
        >
            {/* highlight-end */}
            <Refine
                /* ... */
            >
                <Layout>
                    {/* ... */}
                </Layout>
            </Refine>
            // highlight-next-line
        </ConfigProvider>
    );
};
```

### Use Preset Algorithms

Themes with different styles can be quickly generated by modifying algorithm. Ant Design 5.0 provides three sets of [preset algorithms by default](https://ant.design/docs/react/customize-theme#theme-presets), which are default algorithm `theme.defaultAlgorithm`, dark algorithm `theme.darkAlgorithm` and compact algorithm `theme.compactAlgorithm`. You can switch algorithms by modifying the algorithm property of theme in [`<ConfigProvider/>`](https://ant.design/components/config-provider/#components-config-provider-demo-theme).

[Refer to the Ant Design documentation for more information about customizing Ant Design theme. &#8594](https://ant.design/docs/react/customize-theme#use-preset-algorithms)

#### Switching to dark theme

Let's start with adding a switch to the `Header` component.

```tsx
import { Space, Button } from "antd";

interface HeaderProps {
    theme: "light" | "dark";
    setTheme: (theme: "light" | "dark") => void;
}

const Header: FC<HeaderProps> = (props) => {
    return (
        <Space
            direction="vertical"
            align="end"
            style={{
                padding: "1rem",
            }}
        >
            <Button
                onClick={() => {
                    props.setTheme(props.theme === "light" ? "dark" : "light");
                }}
                icon={props.theme === "light" ? <IconMoonStars /> : <IconSun />}
            />
        </Space>
    );
};

```

Then, we can use the `theme` property of the `ConfigProvider` component to switch between light and dark themes.

```tsx
import { Refine } from "@refinedev/core";
import { ConfigProvider, theme } from "antd";

import { Header } from "./Header";

const App: React.FC = () => {
    // highlight-next-line
    const [currentTheme, setCurrentTheme] = useState<"light" | "dark">("dark");

    return (
        <ConfigProvider
            // highlight-start
            theme={{
                algorithm:
                    currentTheme === "light"
                        ? theme.defaultAlgorithm
                        : theme.darkAlgorithm,
            }}
            // highlight-end
        >
            <Refine
                /* ... */
            >
                <Layout Header={Header}>
                    {/* ... */}
                </Layout>
            </Refine>
        </ConfigProvider>
    );
};
```

:::tip

If you want to customize the default layout elements provided with `@refinedev/antd` package, check out the [Custom Layout](/docs/advanced-tutorials/custom-layout) tutorial.

:::

## Example

<CodeSandboxExample path="customization-theme-antd" />