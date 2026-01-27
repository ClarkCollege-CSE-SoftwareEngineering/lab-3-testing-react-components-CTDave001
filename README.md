# Lab 3: Testing React Components

**Name:** David
**Date:** January 26, 2026

## Reflection

Using `getByRole` and `getByLabelText` improves test reliability compared to `getByTestId` because these queries interact with the DOM the same way users do. When I use `getByRole('button', { name: /add task/i })`, I'm finding the button by its accessible name. If I modify the components internal structure, my tests still pass as long as the user stuff behavior remains the same. With `getByTestId`, I'm getting my tests along to implementation details. If I were to rename or remove a test ID during refactoring, the test breaks even though nothing changed for the user.

I would use `queryBy` instead of `getBy` when I need to assert that an element does NOT exist. For example, after clearing a form error, I used `expect(screen.queryByRole('alert')).not.toBeInTheDocument()`. If I had used `getByRole('alert')` here, the test would throw an error instantly instead of letting me assert that it's not there.

Mocking API calls versus testing against a real backend because of speed, reliability, and realism. Mocked tests run fast, or near instant, and don't depend on network or servers, making them reliable for CI. However, mocks can slowly move from the real API if like the backend changes its response format, the mocked tests wont get it. If you're testing by a real backend, it gives you a higher confidence that the full system works together, but tests become slower because of network issues.

## Key Concepts

- **Query priority:** Prefer `getByRole` > `getByLabelText` > `getByText` > `getByTestId`
- **Query variants:** `getBy` throws if not found, `queryBy` returns null, `findBy` waits asynchronously
- **userEvent over fireEvent:** `userEvent.setup()` simulates real user interactions more accurately
- **Mocking with vi.mock():** Isolate components from dependencies like API modules
- **Testing behavior, not implementation:** Write tests that survive refactoring
