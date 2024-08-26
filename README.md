CLI App in Rust - README
Overview
This CLI application is a simple command-line interface tool designed to manage JIRA-like tasks, including epics and stories. The application is built in Rust and allows users to navigate through different pages, create, update, and delete epics and stories, and maintain the state in a JSON file.

Features
Navigate Between Pages: The application uses a Navigator struct to manage navigation between different pages like HomePage, EpicDetail, and StoryDetail.
CRUD Operations: Users can create, read, update, and delete epics and stories.
State Persistence: The application uses a JSON file to persist the state of epics and stories between sessions.
Error Handling: Errors are gracefully handled using the anyhow crate, ensuring that the application continues running even when issues arise.
Usage
Running the Application
To run the application, execute the following command:

bash
Copy code
cargo run
Navigation
Home Page: The starting point of the application.
Epic Detail Page: Displays details of a specific epic.
Story Detail Page: Displays details of a specific story within an epic.
Navigation Commands:
NavigateToEpicDetail {epic_id}: Navigate to the epic detail page.
NavigateToStoryDetail {epic_id, story_id}: Navigate to the story detail page.
NavigateToPreviousPage: Go back to the previous page.
Exit: Exit the application.
CRUD Operations
Create Epic: Create a new epic.
Update Epic Status: Update the status of an epic.
Delete Epic: Delete an existing epic.
Create Story: Create a new story within an epic.
Update Story Status: Update the status of a story.
Delete Story: Delete a story within an epic.
Error Handling
The application uses anyhow for error handling, providing detailed context in case of failures during CRUD operations or navigation.

Code Structure
Main Components
Navigator: Manages the navigation between pages.
JiraDatabase: Handles database operations, reading, and writing data to a JSON file.
Page Traits: Implements different pages (HomePage, EpicDetail, StoryDetail) as traits.
Example Code
Here’s a snippet showing how the Navigator handles an action:

rust
Copy code
pub fn handle_action(&mut self, action: Action) -> Result<()> {
    match action {
        Action::NavigateToEpicDetail { epic_id } => {
            self.pages.push(Box::new(EpicDetail { epic_id, db: Rc::clone(&self.db) }));
        }
        Action::NavigateToStoryDetail { epic_id, story_id } => {
            self.pages.push(Box::new(StoryDetail { epic_id, story_id, db: Rc::clone(&self.db) }));
        }
        // Other actions...
    }

    Ok(())
}
Testing
The application includes unit tests to ensure functionality, particularly for navigation and CRUD operations.

To run the tests:

bash
Copy code
cargo test
Dependencies
anyhow: For error handling.
serde and serde_json: For JSON serialization and deserialization.
clearscreen: For clearing the terminal screen.
Future Enhancements
User Authentication: Adding user authentication to manage multiple users.
Additional Commands: Expanding the CLI to support more detailed project management features.
Improved UI/UX: Enhancing the terminal interface for a better user experience.
Contributing
Contributions are welcome! Please fork the repository and submit a pull request.
