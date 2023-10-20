# I-LOVE-PDF
it is the simple python code for i love pdf
import requests
PUBLIC_KEY = 'YOUR_PUBLIC_KEY'
SECRET_KEY = 'YOUR_SECRET_KEY'
API_BASE_URL = 'https://api.ilovepdf.com/v1'
def perform_pdf_task(task, input_files, output_file, options={}):
    headers = {
        'Authorization': f'Token {PUBLIC_KEY}:{SECRET_KEY}'
    }
    if task == 1:
        # Combine two or more PDF files into one
        url = f'{API_BASE_URL}/tasks/pdfmerge'
        data = {
            'files': input_files,
        }
    elif task == 2:
        # Separate PDF pages or extract all pages into a PDF
        url = f'{API_BASE_URL}/tasks/pdfsplit'
        data = {
            'range': 'all',
            'files': input_files,
        }
    elif task == 3:
        # Remove PDF password security for reading and editing
        url = f'{API_BASE_URL}/tasks/pdfunlock'
        data = {
            'files': input_files,
        }
    elif task == 4:
        # Extract all text from a PDF file to a TXT file
        url import requests
PUBLIC_KEY = 'YOUR_PUBLIC_KEY'
SECRET_KEY = 'YOUR_SECRET_KEY'
API_BASE_URL = 'https://api.ilovepdf.com/v1'
def perform_pdf_task(task, input_files, output_file, options={}):
    headers = {
        'Authorization': f'Token {PUBLIC_KEY}:{SECRET_KEY}'
    }
    if task == 1:
        # Combine two or more PDF files into one
        url = f'{API_BASE_URL}/tasks/pdfmerge'
        data = {
            'files': input_files,
        }
    elif task == 2:
        # Separate PDF pages or extract all pages into a PDF
        url = f'{API_BASE_URL}/tasks/pdfsplit'
        data = {
            'range': 'all',
            'files': input_files,
        }
    elif task == 3:
        # Remove PDF password security for reading and editing
        url = f'{API_BASE_URL}/tasks/pdfunlock'
        data = {
            'files': input_files,
        }
    elif task == 4:
        # Extract all text from a PDF file to a TXT file
        url = f'{API_BASE_URL}/tasks/text'
        data = {
            'files': input_files,
        }
    elif task == 5:
        # Convert JPG, TIFF, and PNG images to PDF
        url = f'{API_BASE_URL}/tasks/imagepdf'
        data = {
            'files': input_files,
        }

    response = requests.post(url, headers=headers, data=data, files=input_files)
    
    if response.status_code == 200:
        task_id = response.json().get('task')
        download_url = f'{API_BASE_URL}/tasks/{task_id}/download'
        response = requests.get(download_url, stream=True)

        if response.status_code == 200:
            with open(output_file, 'wb') as f:
                for chunk in response.iter_content(1024):
                    f.write(chunk)
            print(f'Task completed. Output saved to {output_file}')
        else:
            print(f'Failed to download the output file. Error: {response.text}')
    else:
        print(f'Task failed. Error: {response.text}')

if _name_ == '_main_':
    task = int(input('Select a task (1-5): '))
    input_files = {'file': open('input.pdf', 'rb')}  # Provide the input files
    output_file = 'output.pdf'  # Define the output file path

    perform_pdf_task(task, input_files, output_file)
