# ![Leadhome](https://www.leadhome.co.za/assets/images/logo.89cf16dfc4c9a7aaa2e15c574b9458f8.svg) Leadhome
## JavaScript style guide
> A mostly reasonable approach to React, Styled Components and ES6

### Basic Rules
- File names must be all lowercase and may use dashes (-), but no additional punctuation
- No unused variables
- Always use === instead of == 
- Always handle the node.js err function parameter
- No defensive coding
- Dont be afraid to use long variable names
- Use prop types!
- Semi colons; Why? 
    ```
    // bad
    console.log('foo')
    [1, 2, 3].forEach(() => console.log('bar'))
    
    // worse 
    console.log('foo')
    ; [1, 2, 3].forEach(() => console.log('bar'))
    
    // good
    console.log('foo');
    [1, 2, 3].forEach(() => console.log('bar'));
    ```
    
### Class vs Stateless
- If you have internal state and/or refs, prefer `class extends React.Component` over `React.createClass`. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

    ```jsx
    // bad
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // good
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
    ```
- And if you don’t have state or refs, prefer arrow functions over classes:

    ```jsx
    // bad
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // good
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );
### Naming
- **Extensions**: Use `.js` extension for React components and Styled Components. Use `.graphql` for GraphQL files
- **Filename**: Use Kebab case for filenames. E.g., `my-component.js`.
- **Component Naming**: Always name components
- **Reference Naming**: Use PascalCase for React components. Use camelCase for functions eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)
- **Styles**: Create style files for your styled components, named `style.js` or `-style.js` appended to the filename
    ```
    // bad
    import reservationCard from './ReservationCard';

    // good
    import ReservationCard from './ReservationCard';

    // bad
    const ReservationItem = <ReservationCard />;

    // good
    const reservationItem = <ReservationCard />;
    ```
- When using map, name your variables, don't use x

### Alignment
- Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [`react/jsx-closing-tag-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

    ```jsx
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>

    // bad
    {showButton &&
      <Button />
    }

    // bad
    {
      showButton &&
        <Button />
    }

    // good
    {showButton && (
      <Button />
    )}

    // good
    {showButton && <Button />}
    ```
### Quotes
- Use single quotes for everything eslint: [`jsx-quotes`](https://eslint.org/docs/rules/jsx-quotes)
- Use template literals if another level of quotation is needed

### Spacing
- 2 spaces – for indentation
- Always include a single space in your self-closing tag. eslint: [`no-multi-spaces`](https://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)
    ```jsx
    // bad
    <Foo/>
    
    // very bad
    <Foo                 />
    
    // bad
    <Foo
     />
    
    // good
    <Foo />
    ```
- Do not pad JSX curly braces with spaces. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)
    ```
    // bad
    <Foo bar={ baz } />
    
    // good
    <Foo bar={baz} />
    ```
- Pad destructured variables with spaces
    ```
    // bad
    import {foo} from 'foo';
    
    // good
    import { foo } from 'foo'
    
    // bad - trailing comma
    import {
      foo,
      bar,
      baz,
    } from 'foo'
    
    // good
    import {
      foo,
      bar,
      baz
    } from 'foo'
    ```
- Do not pad function props with spaces 
    ```
    // bad
    bar = ( query, text ) => foo();
    
    // good
    bar = (query, text) => foo();
    ```
- Dont use brackets with one function prop 
    ```
    // bad
    bar = (query) => foo();
    
    // good
    bar = query => foo();
    ```
- Space after keywords: if & function name
    ```
    // bad 
    if(condition) {}
    
    // good 
    if (condition) {}
    
    // bad
    const myFunc=()=> {};
    
    // good
    const myFunc = () => {};
    ```

### Props
- Always use camelCase for prop names.
- Omit the value of the prop when it is explicitly `true`
### Parentheses
- Wrap JSX tags in parentheses when they span more than one line
    ```
    // bad
    render() {
      return <Food foo="bar">
               <Burger />
             </Food>;
    }
    
    // good
    render() {
      return (
        <Food foo="bar">
          <Burger />
        </Food>
      );
    }
    ```
### Tags
- Always self-close tags that have no children: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)
    ```
    // bad
    <Foo variant="stuff"></Foo>
    
    // good
    <Foo variant="stuff" />
    ```
- If your component has multi-line properties, close its tag on a new line. [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)
    ```
    // bad
    <Foo
      bar="bar"
      baz="baz" />
    
    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```
### Methods
- Use arrow functions always.
- Dont use a constructor unless you need to do some logic in there
    ```
    // bad
    class extends React.Component {
      constructor(props) {
        super(props);
      }
      
      onClickDiv = () => /* some logic */;
      
      render (
        foo();
      );
    }
    
    // good
    class extends React.Component {
      onClickDiv = () => /* some logic */;
      
      render (
        foo();
    );
    ```
### Styled Components
- Destructure variables
    ```
    // bad 
    width: ${props => props.open ? '250px' : '0px'};
    
    // good
    width: ${({ open }) => open ? '250px' : '0px'};
    ```
- Animations
    ```
    const ButtonIconSpinAnimation = keyframes`
      from {
        transform: rotate(0deg);
      }
      to {
        transform: rotate(359deg);
      }
    `;
    
    export const ButtonIconSpin = css`
      animation: ${ButtonIconSpinAnimation} 1s infinite ease-in-out;
    `;
    ```
- Use variables for larger css segments
    ```
    const Bar = css`
      border-color: #F8B24B;
      line-height: 1000000;
    `;

    export const Foo = styled.div`
      ${({baz}) => baz && Bar};
    `;
    ```
