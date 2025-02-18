# Unexpected useEffect Rerenders with Empty Dependency Array

This example demonstrates a subtle bug in React's `useEffect` hook where an effect runs more often than expected, even with an empty dependency array. The issue stems from how closures interact with changing variables inside the component.

## Bug Description:

The `useEffect` hook is designed to run only once after the initial render when given an empty dependency array (`[]`). However, if the effect function references a variable that changes during subsequent renders (despite not being explicitly included in the dependency array), it will re-run.  This often occurs when the effect function closes over a variable that is updated within the component.

## How to Reproduce:

Clone the repository and run `npm start`. Observe the console logs. You'll see that the effect runs repeatedly even though the dependency array is empty.

## Solution:

The solution is to correctly manage the dependencies passed to `useEffect`. If any variables are captured within the effect's function body, and could change later, then they must be explicitly included in the dependency array, thereby making the effect rerun only when those values change.