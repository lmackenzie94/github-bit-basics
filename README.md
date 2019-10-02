# GitHub Bit w/ React Notes

Initialize Bit Workspace: <code>init --package-manager yarn</code>

To track the product list component, we will need to tell Bit about the component and the files that are related to it:

<code>bit add src/components/product-list</code> (can also specify specific files instead of full directory)

You can then run <code>bit status</code> to verify the component was succesfully added

Up to this point, we provided Bit with the source file of the component. But in order to consume the files in other projects, the component needs to be built.
To do so, install the React compiler <code>bit import bit.envs/compilers/react --compiler</code>.

Next, <code>bit build</code>

Building the component serves two purposes:

- Make the component directly consumable by other projects.
- Make sure that the component is all-inclusive and contains all the parts that are required in order to share it with others.

Right now the component lives inside your project and may consume some dependencies from your project. Bit build is taking place in an isolated environment to make sure the process will also succeed on the cloud or in any other project

Next, export the component by running <code>bit tag --all 0.0.1</code> and then <code>bit export [username].[collection]</code>

- this command tags all components that are currently staged in Bit. (again, run <code>bit status</code> to make sure everything went smoothly)

To see all the components you have, run <code>bit list</code>

Use <code>bit show [componentName]</code> to see details about your component (id, compiler, dependencies, etc)

If you make changes to a component, run <code>bit build</code>, then <code>bit tag [component-id]</code>, then <code>bit export [username].[collection]</code>

To add dependencies that bit doesn't pick up, in "bit" object of package.json, add something like:

<pre>
"overrides": {
      "*": {
        "dependencies": {
          "@emotion/core": "+",
          "@mdx-js/react": "+"
        }
      }
    },
</pre>
