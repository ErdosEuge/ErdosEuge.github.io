---
layout: default
---

# Projects

This section show and describe my main projects done so fare both in my accademic and professional life as a Statistician and Data Scientist.

<div id="projects-container"></div>

<script>
    // Fetch and display projects
    fetch('/assets/data/projects.json')
        .then(response => response.json())
        .then(projects => {
            const container = document.getElementById('projects-container');
            
            // Group projects by year
            const projectsByYear = projects.reduce((acc, project) => {
                // Handle comma-separated years
                const years = project.Year.toString().split(',').map(y => y.trim());
                years.forEach(year => {
                    if (!acc[year]) {
                        acc[year] = [];
                    }
                    acc[year].push(project);
                });
                return acc;
            }, {});

            // Sort years in descending order
            const sortedYears = Object.keys(projectsByYear).sort((a, b) => b - a);

            // Create HTML for each year
            sortedYears.forEach(year => {
                const yearSection = document.createElement('div');
                yearSection.className = 'year-section';
                yearSection.innerHTML = `<h2>${year}</h2>`;

                // Sort projects within each year by name
                projectsByYear[year].sort((a, b) => a.Name.localeCompare(b.Name))
                    .forEach(project => {
                        const projectDiv = document.createElement('div');
                        projectDiv.className = 'project-card';
                        projectDiv.innerHTML = `
                            <h3>${project.Name}</h3>
                            <p><strong>Description:</strong> ${project.Description}</p>
                            <p><strong>Domain:</strong> ${project.Domain}</p>
                            <p><strong>Stakeholder:</strong> ${project.Stakeholder}</p>
                            <p><strong>Programming Languages:</strong> ${project.Programming_Languages}</p>
                            <p><strong>Tools:</strong> ${project.Tools}</p>
                            <p><strong>Algorithms:</strong> ${project.Algorithms}</p>
                        `;
                        yearSection.appendChild(projectDiv);
                    });

                container.appendChild(yearSection);
            });
        })
        .catch(error => console.error('Error loading projects:', error));
</script>

<style>
    .year-section {
        margin-bottom: 2em;
    }
    .project-card {
        border: 1px solid #ddd;
        border-radius: 8px;
        padding: 1em;
        margin: 1em 0;
        background-color: #f9f9f9;
    }
    .project-card h3 {
        margin-top: 0;
        color: #333;
    }
    .project-card p {
        margin: 0.5em 0;
    }
</style>

[back](../)