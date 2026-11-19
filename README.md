# AnswerStyle

AnswerStyle provides styles and browser behavior for semantic HTML. Add a named attribute to opt into a component's appearance. Use native elements and state for interaction and accessibility.

```html
<article card stack>
  <h2>Workspace</h2>
  <p>Invite someone to work with you.</p>
  <div cluster>
    <button btn type="button">Invite</button>
    <a btn btn-variant="secondary" href="/members">Members</a>
  </div>
</article>
```

The npm and Python packages are not published yet; see [DEV.md](DEV.md) for local development setup. JavaScript apps import `@answerdotai/answerstyle/styles.css` once. Svelte components emit the same attributes as the HTML above.

In Python, `from answerstyle import assets` gives the package's browser assets. Serve that directory and link `styles.css`. The stylesheet does not need a script. The browser modules `fit.js`, `floating.js`, `interactions.js` and `copy.js` are available separately. Native dropdowns use normal links and controls; tooltips use CSS. Shared controllers add fitting, popover placement, tabs and toolbar focus where needed.

The [notebooks](nbs/) explain the palette, typography, layout and components and include working previews. See [DEV.md](DEV.md) for the source build.

