<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Builder</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="form-container">
        <h1>Custom Form Builder</h1>
        <form id="customForm">
            <div id="formBuilder">
                <!-- Dynamic form elements will be added here -->
            </div>
            <button type="button" id="addField">Add Field</button>
            <button type="submit">Submit</button>
        </form>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    margin: 20px;
    padding: 0;
    background-color: #f4f4f4;
}

.form-container {
    max-width: 600px;
    margin: auto;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
}

button {
    margin: 10px 0;
    padding: 10px 15px;
    border: none;
    background: #007BFF;
    color: white;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
}

button:hover {
    background: #0056b3;
}

input, select, textarea {
    display: block;
    width: 100%;
    margin: 10px 0;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.dynamic-field {
    display: flex;
    align-items: center;
    gap: 10px;
}

.dynamic-field button {
    background: #dc3545;
    margin-left: 10px;
}

.dynamic-field button:hover {
    background: #a71d2a;
}

document.addEventListener("DOMContentLoaded", () => {
    const formBuilder = document.getElementById("formBuilder");
    const addFieldButton = document.getElementById("addField");

    addFieldButton.addEventListener("click", () => {
        const fieldContainer = document.createElement("div");
        fieldContainer.className = "dynamic-field";

        const label = document.createElement("input");
        label.type = "text";
        label.placeholder = "Field Label";
        label.required = true;

        const fieldType = document.createElement("select");
        fieldType.innerHTML = `
            <option value="text">Text</option>
            <option value="email">Email</option>
            <option value="number">Number</option>
            <option value="textarea">Textarea</option>
        `;

        const removeButton = document.createElement("button");
        removeButton.type = "button";
        removeButton.innerText = "Remove";
        removeButton.addEventListener("click", () => {
            fieldContainer.remove();
        });

        fieldContainer.appendChild(label);
        fieldContainer.appendChild(fieldType);
        fieldContainer.appendChild(removeButton);

        formBuilder.appendChild(fieldContainer);
    });

    const form = document.getElementById("customForm");
    form.addEventListener("submit", (event) => {
        event.preventDefault();
        const fields = formBuilder.querySelectorAll(".dynamic-field");

        let formData = [];
        fields.forEach(field => {
            const label = field.querySelector("input").value;
            const type = field.querySelector("select").value;

            formData.push({ label, type });
        });

        console.log("Generated Form Data:", formData);
        alert("Form submitted! Check the console for form data.");
    });
});

<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $formData = $_POST['formData'];
    $decodedData = json_decode($formData, true);

    // Process the form data
    foreach ($decodedData as $field) {
        echo "Label: " . htmlspecialchars($field['label']) . " - Type: " . htmlspecialchars($field['type']) . "<br>";
    }

    // Return a response
    echo "Form submitted successfully!";
}
?>
