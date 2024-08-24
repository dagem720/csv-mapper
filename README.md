# Project Name

This project uses Vue 3 and Tailwind CSS. It consists of two components: a CSV Mapper Table component and a File Upload component. The CSV Mapper component automatically extracts headers and data from the uploaded file and displays it in a table format.

## Deployment

The project is deployed on Vercel. You can access the deployed version [csv-mapper-henna.vercel.app](#)

## Components

### 1. CSV Mapper Table Component

The CSV Mapper Table component is responsible for parsing the uploaded CSV file and displaying the extracted data in a table format. It automatically extracts headers and data from the file.

### 2. File Upload Component

The File Upload component allows users to select a CSV file for processing. Once a file is selected, the CSV Mapper Table component processes the file and displays its contents.

you can get the sample file in the repo file.csv

## Getting Started

To run this project locally, follow these steps:

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Start the development server using `npm run serve`.

## Project Structure

project-directory/
│
├── src/
│ ├── components/
│ │ ├── CSVMapper.vue
│ │ ├── uploadFileModal.vue
│ │
│ ├── App.vue
│ ├── main.js
│
├── public/
│ ├── index.html
│
├── README.md
├── package.json

## Local Development

1. Clone the repository:

```bash
git clone https://github.com/dagem720/csv-mapper
cd csv-mapper
```
