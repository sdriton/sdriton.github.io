---
layout: default
title: User Guide
permalink: /confomeety/
nav_order: 10
---

# Confomeety User Guide

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [Managing Boards](#managing-boards)
4. [Managing Meetings](#managing-meetings)
5. [Managing Agenda](#managing-agenda)
6. [Using Tags](#using-tags)
7. [Dashboard Overview](#dashboard-overview)
8. [Reports and Email](#reports-and-email)
9. [Configuration](#configuration)
10. [Tips and Best Practices](#tips-and-best-practices)


## Introduction

### What is Confomeety?

Confomeety is a comprehensive meeting and agenda management application designed to help organizations efficiently manage meetings for boards, committees, task forces, projects and many more. It provides a structured workflow for organizing meetings, tracking agenda items, and documenting decisions.

### Key Features

- **Board Management**: Create and manage boards, committees, and projects with custom configurations
- **Meeting Scheduling**: Schedule meetings with date, time, location, and participants
- **Agenda Management**: Create detailed agenda items (topics) with presenters, goals, and time allocations
- **Status Tracking**: Track the approval status of topics and meeting progress
- **File Attachments**: Attach relevant documents to meetings and agenda items
- **Email Reports**: Send meeting minutes and reports via email
- **Calendar Integration**: View meetings in calendar format
- **Dashboard Analytics**: Visualize meeting metrics and statistics
- **Multi-Company Support**: Separate data by company for enterprise deployments

### User Roles

- **User**: Can view and manage meetings and topics
- **Manager**: Has full access including configuration settings and board creation

![Confomeety Main Interface](/assets/confomeety_boards.png)


## Getting Started

### Accessing Confomeety

1. Log in to your Odoo instance
2. Click on the **Confomeety** app icon from the main menu
3. You will see the main dashboard with recent meetings and statistics

![Confomeety App Menu](/assets/confomeety_menu.png)

### Navigation Overview

The Confomeety application has the following main menu items:

- **Dashboard**: Overview of meetings, statistics, and key metrics
- **Boards**: List and manage all boards, committees, and projects
- **Meetings**: Schedule and manage meetings
- **Topics**: View and manage all agenda items
- **Configuration** (Managers only): Customize board types, topic categories, statuses, and goals

### Understanding the Workflow

Confomeety follows a hierarchical structure:

```
Board (Committee/Project)
  └── Meeting
       └── Topics (Agenda Items)
            ├── Presenters
            ├── Files
            ├── Status
            └── Notes/Minutes
```

**Typical Workflow:**
1. Create or select a Board
2. Schedule a Meeting for that Board
3. Add Topics to the Meeting
4. Conduct the meeting and update topic statuses
5. Add notes and decisions
6. Set Meeting Status to **Done**


## Managing Boards

### What is a Board?

A Board represents an organizational structure such as:
- Board of Directors
- Executive Committee
- Project Team
- Working Group
- Advisory Board

Each board has its own meetings, custom topic categories, and status configurations.

### Creating a New Board

> **Prerequisites:** You must have Manager permissions to create boards.

1. Navigate to **Confomeety > Boards**
2. Click the **Create** button
3. Fill in the required information:
   - **Name**: Give your board a clear, descriptive name
   - **Type**: Select the board type (Board, Committee, Group, or Project)
   - **Description**: Add details about the board's purpose and scope
   - **Company**: Select the company (for multi-company setups)
4. (Optional) Upload a **Board Logo** by clicking on the image placeholder
5. Click **Save**

![Creating a Board](/assets/create_board.png)

### Viewing Board Details

1. Navigate to **Confomeety > Boards**
2. Click on a board name to open its detail view

The board detail page shows:
- Board information (name, type, description, logo)
- **Meetings** tab: All meetings associated with this board
- Statistics: Meeting count
- Chatter: Track communications and activities

### Editing a Board

**Prerequisites:** Manager permissions required.

1. Open the board detail view
2. Click **Edit**
3. Modify the fields as needed
4. Click **Save**

### Archiving a Board

Instead of deleting boards, you can archive them:

1. Open the board detail view
2. Click the **Action** menu (![action_gear](/assets/action_gear.png))
3. Select **Archive**
4. Confirm the action

To view archived boards:
1. Go to **Confomeety > Boards**
2. Click the **Filters** button
3. Select **Archived**


## Managing Meetings

### Creating a New Meeting

1. Navigate to **Confomeety > Meetings**
2. Click **Create**
3. Fill in the meeting details:
   - **Title**: Meeting name (e.g., "Monthly Board Meeting")
   - **Board**: Select the board this meeting belongs to
   - **Date and Time**: Set the start date and time
   - **End**: Set the end time (automatically calculated based on duration)
   - **Duration**: Specify meeting length in hours
   - **Location**: Enter meeting location (room, office, or virtual meeting link)
4. (Optional) Add **Tags** to categorize the meeting
5. Click **Save**

![Creating a Meeting](/assets/create_meeting.png)



### Meeting Status Workflow

Meetings progress through the following statuses:

1. **Draft**: Initial state when creating a meeting
2. **Confirmed**: Meeting is scheduled and confirmed
3. **In Progress**: Meeting is currently happening
4. **Done**: Meeting has concluded
5. **Cancelled**: Meeting was cancelled

To change the meeting status:
- Click the status buttons at the top of the meeting form
- Or set the **Status** field in the form


### Adding Topics to a Meeting

There are two ways to add topics (agenda items) to a meeting:

#### Method 1: From the Meeting Form

1. Open the meeting
2. Click **Edit**
3. Go to the **Topics** tab
4. Click **Add a line**
5. Fill in the topic details
6. Click **Save**

#### Method 2: Create Topic Separately

1. Click the **Topics** button on the meeting form (shows count badge)
2. Click **Create**
3. Fill in the topic details
4. The topic is automatically linked to the meeting

### Viewing Meeting Calendar

1. Navigate to **Confomeety > Meetings**
2. Click the **Calendar** view button (calendar icon)
3. View meetings by Day, Week, or Month
4. Click on a meeting to open its details
5. Drag and drop to reschedule meetings

![Meeting Calendar View](/assets/meetings_calendar_view.png)

### Adding Meeting Files

Attach documents relevant to the meeting:

1. Open the meeting
2. Click **Edit**
3. Scroll to the **Files** section
4. Click **Attach Files**
5. Select file(s) from your computer or drag and drop
6. Click **Save**

### Adding Meeting Notes

Document meeting minutes and decisions:

1. Open the meeting
2. Click **Edit**
3. Scroll to the **Notes** section
4. Use the rich text editor to add:
   - Meeting minutes
   - Decisions made
   - Action items
   - Follow-up tasks
5. Use formatting tools (bold, italic, lists, tables)
6. Click **Save**


## Managing Agenda

### What is a Topic?

A Topic is an individual agenda item that will be discussed during a meeting. Topics include:
- Subject/title
- Category
- Goal/purpose
- Duration
- Presenter(s)
- Supporting documents
- Status tracking
- Notes and decisions
- Tags

### Who Can Create Topics

By default **Confomeety Manager** group can manage all the Confomeety resources including Topics. The **Confomeety User** group can **create** topics, **modify** and **delete** their own **Topics**.

If needed, permissions can be modified in Odoo to address your own scenario.

### Creating a New Topic

1. Navigate to **Confomeety > Topics**
2. Click **Create**
3. Fill in the required information:

#### Basic Information
- **Subject**: Topic title (e.g., "Q1 Financial Results Review")
- **Board**: Select the board
- **Meeting**: Select the meeting this topic belongs to
- **Category**: Choose appropriate category (e.g., Presentation, Sales, Briefing)
- **Goal**: Select the purpose (Decide, Consult, Inform, or Other)

#### Time Allocation
- **Duration**: Specify time allocation in hours (e.g., 0.5 for 30 minutes)
- **Sequence**: Order in the agenda (lower numbers appear first)

#### Presenters
- **Presenters**: Select one or more users who will present this topic
- Click on the **Presenters** field and start typing the name of the user. Repeat to add multiple presenters.

#### Additional Details
- **Subject Link**: URL to related documents or presentations
- **Status**: Current status (Approved, Rejected, Pending, etc.)
- **Tags**: Add tags for categorization

4. Click **Save**

![Creating a Topic](/assets/create_topic.png)

### Viewing Topics in Different Views

#### List View
- Shows all topics with key information
- Sort by clicking column headers
- Search and filter topics

#### Kanban View
1. Navigate to **Confomeety > Topics**
2. Click the **Kanban** view button (grid icon)
3. Topics are grouped by **Status**
4. Drag and drop topics between status columns to update their status

#### Form View
- Detailed view of a single topic
- Access by clicking on a topic in list or kanban view

### Attaching Files to Topics

1. Open the topic
2. Click **Edit**
3. Go to the **Files** section
4. Click **Attach Files**
5. Select documents (presentations, reports, supporting materials)
6. Click **Save**

The **file count** badge shows the number of attached files.

### Adding Topic Notes

Document the discussion and decisions for each topic:

1. Open the topic
2. Click **Edit**
3. Scroll to the **Notes** section
4. Enter:
   - Discussion summary
   - Decisions made
   - Action items
   - Responsible parties
   - Deadlines
5. Use the rich text editor for formatting
6. Click **Save**

### Opening Topic Links

If a topic has a **Subject Link** or has **attached files**:

1. Open the topic
2. Click the **Open Link** button (🔗 icon) in the form
3. The link opens in a new browser tab

This is useful for linking to:
- Online presentations (Google Slides, PowerPoint Online)
- Shared documents
- Project management tools
- Reference materials

### Sequencing Topics

![Sequence Topics](/assets/sequence_topics.png)

Control the order of topics in the agenda:

1. Open the topic list whether on the meeting detail or the topics list
2. Click on the ![move_icon](/assets/move_icon.png)
 icon that is located in the beggining of the topic item and drag the topic to the desired position
3. Click **Save**

In the Kanban view, just click and drag the topic card to the desired position.

## Using Tags

### What are Tags?

Tags help you categorize and filter both meetings and topics. They are completely customizable and can represent:
- Project names
- Departments
- Priority levels
- Subject areas
- Custom classifications

### Types of Tags

- **Meeting Tags**: Used to categorize meetings
- **Topic Tags**: Used to categorize agenda items

### Creating Tags

> **Prerequisites:** Manager permissions may be required depending on security settings.

1. Navigate to any meeting or topic form
2. In the **Tags** field, start typing a new tag name
3. Click **Create "Tag Name"** or press **Enter** key
4. The tag is created and applied

Alternatively:
1. Navigate to any meeting or topic form
2. In the **Tags** field, click on the dropdown arrow
3. Click **Search more**, a dialog opens
4. Click **New**
5. Enter:
   - **Name**: Tag name
   - **Company**: Select company (or leave blank for all companies)
   - **Color**: Select a color for visual distinction
   
4. Click **Save**

### Using Tags to Filter

![Using Tags Filter](/assets/filters.png)

#### In List View
1. Navigate to **Confomeety > Meetings** or **Topics**
2. Type in the search bar
3. Click **Search Tags**
4. Select one or more tags
5. View filtered results

#### Creating Saved Filters
1. Apply your desired filters (tags, dates, boards, etc.)
2. Click **Favorites** (star icon)
3. Click **Save current search**
4. Name your filter
5. Check options:
   - **Use by default**: Apply this filter when opening this view
   - **Share with all users**: Make available to all users
6. Click **Save**


## Dashboard Overview

![Dashboard Overview](/assets/confomeety_dashboard.png)

### Accessing the Dashboard

1. Navigate to **Confomeety > Dashboard**
2. View key metrics and statistics

### Dashboard Components

The Confomeety dashboard provides an overview of your meeting activities:

#### Key Performance Indicators (KPIs)

- **Total Meetings**: Count of all scheduled meetings
- **Upcoming Meetings**: Meetings scheduled for the near future
- **Meetings This Month**: Current month's meeting count
- **Total Topics**: Count of all agenda items
- **Pending Topics**: Topics awaiting approval or decision
- **Active Boards**: Number of active boards/committees

#### Charts and Visualizations

- **Meetings by Status**: Pie or bar chart showing meeting distribution by status
- **Topics by Category**: Breakdown of agenda items by category
- **Meeting Timeline**: Calendar or timeline view of upcoming meetings
- **Board Activity**: Meetings per board

#### Recent Activity

- Recently created meetings
- Recently updated topics
- Upcoming meetings (next 7 days)

### Customizing Your Dashboard

Besides the default Dashboard provided by **Confomeety**, which in most cases, is adequate for an organization, other **Odoo Dashboards** can be created and used depending on your needs.

Depending on your Dashboard module and Odoo version and configuration, you may be able to:
- Add KPIs and Graphs
- Rearrange dashboard widgets
- Show/hide specific KPIs
- Adjust date ranges
- Export data

## Reports and Email

### Viewing Meeting Report

1. Open a meeting
2. Scroll to the **Notes** section
3. View the formatted meeting report with:
   - Meeting details
   - Agenda topics
   - Notes and decisions
   - Attached files

### Sending Meeting Report by Email

1. Open a meeting
2. Click **Edit**
3. Ensure the **Notes** section contains the meeting report
4. Click **Save**
5. Click the **Send By Email** button
6. A pre-filled email composer opens with:
   - **Subject**: "Meeting Minutes: [Meeting Title]"
   - **Body**: Formatted meeting report with all topics
   - **Recipients**: Board members and presenters (depending on configuration)
7. Review the email
8. Add or remove recipients
9. Modify the message if needed
10. Click **Send**

### Email Template

The meeting report email includes:
- Meeting title and details
- Date, time, and location
- Board information
- All agenda topics with:
  - Subject
  - Category and goal
  - Presenters
  - Duration
  - Status
  - Notes/decisions
- Meeting notes
- Attached files (as email attachments)

### Printing Reports

1. Open a meeting or topic
2. Click **Print/PDF**
3. Select the report format
4. The PDF report is generated
5. Print or save the PDF


## Configuration

**Note:** Configuration options are only available to users with Manager permissions.

### Accessing Configuration

Navigate to **Confomeety > Configuration**

The configuration menu includes:
- **Board Types**
- **Topic Categories**
- **Topic Statuses**
- **Topic Goals**

### Managing Board Types

Board types classify the nature of your organizational structures.

#### Default Board Types
- Board
- Committee
- Group
- Project

#### Creating a Custom Board Type

1. Navigate to **Confomeety > Configuration > Board > Board Types**
2. Click **Create**
3. Enter:
   - **Name**: Type name (e.g., "Task Force", "Advisory Panel")
   - **Active**: Check to make it available
4. Click **Save**

### Managing Topic Categories

Categories classify the type of agenda items.

#### Default Categories
- Market Analysis
- Presentation
- Solution Architecture
- Briefing
- Performance Review
- Sales
- Employee Hiring
- Other

#### Creating a Custom Category

1. Navigate to **Confomeety > Configuration > Topic > Topic Categories**
2. Click **Create**
3. Enter:
   - **Name**: Category name (e.g., "Budget Review", "Strategic Planning")
   - **Board**: (Optional) Restrict this category to a specific board
   - **Company**: Select company or leave blank for all companies
   - **Color**: Select a visual color
   - **Sequence**: Order in dropdown lists
   - **Active**: Check to make it available
4. Click **Save**

#### Board-Specific Categories

You can create categories that are only available for specific boards:

1. Create a new category
2. Set the **Board** field to a specific board
3. This category will only appear when creating topics for that board


### Managing Topic Statuses

Statuses track the approval or decision status of agenda items.

#### Default Statuses
- Approved
- Approved (Preliminary)
- Rejected
- Pending
- Other

#### Creating a Custom Status

1. Navigate to **Confomeety > Configuration > Topic > Topic Statuses**
2. Click **Create**
3. Enter:
   - **Name**: Status name (e.g., "Under Review", "Deferred", "Needs Info")
   - **Board**: (Optional) Restrict to a specific board
   - **Company**: Select company or leave blank
   - **Color**: Select a color for Kanban view
   - **Sequence**: Order in dropdown and Kanban columns
   - **Active**: Check to make it available
4. Click **Save**

### Managing Topic Goals

Goals define the purpose or objective of agenda items.

#### Default Goals
- Decide: Requires a decision from the board
- Consult: Seeking input and feedback
- Inform: Informational only, no action required
- Other: Custom purposes

#### Creating a Custom Goal

1. Navigate to **Confomeety > Configuration > Topic > Topic Goals**
2. Click **Create**
3. Enter:
   - **Name**: Goal name (e.g., "Approve", "Review", "Discuss")
   - **Board**: (Optional) Restrict to a specific board
   - **Company**: Select company or leave blank
   - **Sequence**: Order in dropdown lists
   - **Active**: Check to make it available
4. Click **Save**

### Best Practices for Configuration

1. **Keep it Simple**: Don't create too many categories or statuses; keep lists manageable
2. **Be Consistent**: Use clear, consistent naming conventions
3. **Use Colors Wisely**: Assign meaningful colors (e.g., green for approved, red for rejected)
4. **Board-Specific Options**: Create board-specific categories/statuses only when necessary
5. **Review Periodically**: Archive unused options to keep lists clean


## Tips and Best Practices

### Meeting Planning

1. **Schedule in Advance**: Create meetings at least one week in advance
2. **Use Clear Titles**: Include the meeting title (e.g., "Advisory Board Meeting")
3. **Set Realistic Durations**: Add buffer time for discussions
4. **Add Location Details**: Include room numbers or virtual meeting links

### Agenda Management

1. **Create Topics Early**: Add agenda items before the meeting
2. **Assign Presenters**: Ensure presenters are notified
3. **Allocate Time Wisely**: Be realistic about topic durations
4. **Sequence Logically**: Order topics from most to least important
5. **Attach Materials Early**: Upload presentations and documents in advance

### During Meetings

1. **Update Status**: Change meeting status to "In Progress"
2. **Take Notes**: Document decisions and discussions in real-time
3. **Update Topic Status**: Mark topics as approved/rejected during the meeting
4. **Track Action Items**: Use notes to record who is responsible for what

### After Meetings

1. **Complete Notes**: Fill in any missing information
2. **Attach Final Files**: Upload finalized presentations or documents
3. **Send Report**: Email the meeting minutes to participants
4. **Update Status**: Change meeting status to "Done"
5. **Create Follow-up Items**: Create topics for the next meeting based on action items

### Organization

1. **Use Tags Consistently**: Develop a standard tagging system
2. **Archive Old Meetings**: Keep the active list manageable
3. **Regular Cleanup**: Archive or delete draft meetings that won't occur
4. **Naming Conventions**: Use consistent naming for boards and meetings

### Security and Permissions

1. **Limit Manager Access**: Only assign manager role to trusted users
2. **Review Regularly**: Periodically review who has access to sensitive boards
3. **Use Company Separation**: In multi-company setups, ensure proper data separation
4. **Use Different Companies** for **Organizational Units** or **Departments** that require restricted user access to the Board information and assign the Company to the allowed Users.

### Performance

1. **Limit File Sizes**: Compress large files before attaching
2. **Use Links**: For very large documents, use Subject Link instead of attachments
3. **Archive Old Data**: Archive meetings and topics from previous years

### Collaboration

1. **Use Chatter**: Communicate with team members using the message thread
2. **Assign Activities**: Create follow-up tasks and assign to responsible parties
3. **Share Filters**: Create and share useful saved filters with your team
4. **Meeting Reminders**: Use Odoo's activity system to set reminders


## Keyboard Shortcuts

Odoo provides several keyboard shortcuts to speed up your work:

- **Ctrl+K** (Cmd+K on Mac): Open command palette
- **Ctrl+S** (Cmd+S on Mac): Save current form
- **Ctrl+/**: Discard changes
- **Alt+N**: Create new record (when in list view)
- **Alt+E**: Edit current record
- **Alt+P**: Print
- **Esc**: Close dialog or return to list view

## Troubleshooting

### I can't create a board

**Solution**: Only users with Manager permissions can create boards. Contact your system administrator to request access.

### A meeting doesn't appear in the calendar

**Solution**: Ensure the meeting has a start date/time set and the status is not "Cancelled". Check your filters are not hiding the meeting.

### I can't change the topic status

**Solution**: Only managers can modify the status field. If you need to update a topic status, contact a manager or use the Kanban view drag-and-drop if permitted.

### Topics aren't appearing in the meeting

**Solution**: Ensure the topic's Board and Meeting fields match. A topic must belong to the same board as the meeting.

### Email reports aren't sending

**Solution**: 
1. Verify your Odoo email server is configured
2. Check that recipients have valid email addresses
3. Ensure you have saved the meeting notes before sending
4. Contact your system administrator if issues persist

### Files aren't attaching

**Solution**:
1. Check file size limits (typically 25MB)
2. Ensure you have sufficient storage quota
3. Try a different file format
4. Contact your administrator if the issue persists


## Support and Resources

### Need Help?

- **Contact Support**: Reach out to DS Solutions for technical support
- **Training**: Request user training sessions for your team
- **Documentation**: Refer to this guide and the API documentation

### API Integration

Confomeety provides a comprehensive REST API for integration with other systems. See the **API Documentation** for details.

### Feedback

We welcome your feedback! Contact DS Solutions to suggest improvements or report issues.

---

## Appendix

### Glossary

- **Board**: An organizational structure (board, committee, project, group)
- **Meeting**: A scheduled gathering with agenda items
- **Topic**: An individual agenda item to be discussed in a meeting
- **Presenter**: A user who will present or lead discussion on a topic
- **Status**: The approval or decision state of a topic
- **Category**: The type or classification of a topic
- **Goal**: The purpose or objective of a topic
- **Chatter**: The message thread and activity panel in Odoo forms
- **Kanban**: A visual board view with cards grouped by status
- **Tag**: A label used to categorize and filter records

### Workflow Diagram
![Confomeety Flow](/assets/confomeety_flow.png)


---

**Document Version**: 1.0  
**Confomeety Version**: 19.0.1.0.0  
**© 2026 DS Solutions. All rights reserved.**
