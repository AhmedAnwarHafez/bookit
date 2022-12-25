# 👻 Bookit 👻

[Demo](https://bookit.leveluptutorials.com/book)
Docs (coming soon)

## The least spooky way to build your components.

Pronounced Boo-Kit or Book-It

A new Story environment with a different approach. Finely tuned to work directly within your Svelte Kit projects. Stay tuned for more information and docs on how to use and add to your projects.

### Why it's dope

- Easy
- Build for Svelte Kit
- No webpack, or extra build process
- Integrated into your app
- Themeable
- Use your real data
- Simple

### Setting up your project

You'll need to create this route structure

1. First step is to create this new route structure
    ```diff
    src/routes/
    ├─ +layout.svelte
    ├─ ...                  // other routes
    +└─ (book)/
    +    ├─ +layout.svelte  
    +    ├─ +layout.ts
    +    └─ book/
    +        └─ [parent]-[title]/
    +            ├─ +page.svelte
    +            └─ +page.ts
    ```

    - In `src/routes/(book)/+layout.svelte`

        ```html
        <script lang="ts">
            import { Book } from '@leveluptuts/bookit';
            import '../../../src/app.css'; // your app's css
        </script>

        <Book>
            <slot />
        </Book>
        ```
    - In `src/routes/(book)/+layout.svelte`
        ```js
        export { layoutLoad as load } from '@leveluptuts/bookit';
        ```
    - In `src/routes/(book)/book/[parent][title]/+page.svelte`
        ```html
        <script lang="ts">
            import { Bookit } from '@leveluptuts/bookit';
            type Data = {
                props: {
                    params: {
                        parent: string;
                        title: string;
                    };
                };
            };
            export let data: Data;
        </script>

        <Bookit params={data.props.params} />
        ```
    - In `src/routes/(book)/book/[parent]-[title]/+page.ts`
        ```js
        export { load } from '@leveluptuts/bookit';
        ```
2. Now your project is set up, let's now create our first story file that has a name like this `MyButton.story.svelte`

3. Import and wrap your component with `Canvas` and `Frame`

    ```html
    <script context="module" lang="ts">
        import { Canvas, Frame } from '@leveluptuts/bookit';
        import MyButton from './MyButton.svelte';

        export const parent = 'Library';
        export const title = 'Button';
    </script>

    <Canvas>
        <Frame title="Primary">
            <MyButton color="blue" />
        </Frame>
    </Canvas>
    ```
4. To view the story in the browser, navigate to `/book/Library-Button`.

**Note:** Both variables in the story `parent` and `title` are used for the paramterized route in `/book/[parent]-[title]`