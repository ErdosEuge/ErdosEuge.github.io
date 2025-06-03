---
layout: default
---

# Projects

This section show and describe my main projects done so fare both in my accademic and professional life as a Statistician and Data Scientist.

<!-- Bubble Chart Container -->
<div id="bubble-chart" style="width: 100%; height: 500px; margin-bottom: 2em;"></div>

<script>
    // Fetch data and create bubble chart
    fetch('/assets/data/Projects_v2.json')
        .then(response => response.json())
        .then(data => {
            // Create traces for each domain
            const domains = [...new Set(data.map(item => item.Domain))];
            const traces = domains.map(domain => {
                const domainData = data.filter(item => item.Domain === domain);
                return {
                    x: domainData.map(item => item.Year),
                    y: domainData.map(item => item["# Line of Code"]),
                    mode: 'markers',
                    name: domain,
                    text: domainData.map(item => item.Name),
                    marker: {
                        size: domainData.map(item => item.Months * 5), // Scale bubble size
                        sizemode: 'area',
                        sizeref: 2 * Math.max(...domainData.map(item => item.Months)) / (40**2),
                        sizemin: 4
                    },
                    hovertemplate: 
                        '<b>%{text}</b><br>' +
                        'Year: %{x}<br>' +
                        'Lines of Code: %{y}<br>' +
                        'Months: %{marker.size/5}<br>' +
                        '<extra></extra>'
                };
            });

            const layout = {
                title: 'Project Timeline and Scale',
                xaxis: {
                    title: 'Year',
                    gridcolor: 'lightgray',
                    zerolinecolor: 'lightgray'
                },
                yaxis: {
                    title: 'Lines of Code',
                    gridcolor: 'lightgray',
                    zerolinecolor: 'lightgray'
                },
                hovermode: 'closest',
                showlegend: true,
                legend: {
                    x: 1,
                    xanchor: 'right',
                    y: 1
                },
                paper_bgcolor: 'rgba(0,0,0,0)',
                plot_bgcolor: 'rgba(0,0,0,0)'
            };

            Plotly.newPlot('bubble-chart', traces, layout);
        })
        .catch(error => console.error('Error loading chart data:', error));
</script>

<div id="projects-container"></div>

<script>
    // Fetch and display projects
    fetch('/assets/data/projects.json')
        .then(response => response.json())
        .then(projects => {
            const container = document.getElementById('projects-container');
            
            // Group projects by year
            const projectsByYear = projects.reduce((acc, project) => {
                const year = project.Year.toString();
                if (!acc[year]) {
                    acc[year] = [];
                }
                acc[year].push(project);
                return acc;
            }, {});

            // Sort years in descending order
            const sortedYears = Object.keys(projectsByYear).sort((a, b) => b - a);

            // Create HTML for each year
            sortedYears.forEach(year => {
                const yearSection = document.createElement('div');
                yearSection.className = 'year-section';
                yearSection.innerHTML = `<h2>${year}</h2>`;

                // For 2018, put Insurance-based Recommender System first
                if (year === '2018') {
                    const otherProjects = projectsByYear[year].filter(p => p.Name !== 'Insurance-based Recommender System');
                    const insuranceProject = projectsByYear[year].find(p => p.Name === 'Insurance-based Recommender System');
                    
                    // Display Insurance project first
                    if (insuranceProject) {
                        const projectDiv = document.createElement('div');
                        projectDiv.className = 'project-card';
                        projectDiv.innerHTML = `
                            <h3>${insuranceProject.Name}</h3>
                            <p><strong>Description:</strong> ${insuranceProject.Description}</p>
                            <p><strong>Domain:</strong> ${insuranceProject.Domain}</p>
                            <p><strong>Stakeholder:</strong> ${insuranceProject.Stakeholder}</p>
                            <p><strong>Programming Languages:</strong> ${insuranceProject["Programming Languages"]}</p>
                            <p><strong>Tools:</strong> ${insuranceProject.Tools}</p>
                            <p><strong>Algorithms:</strong> ${insuranceProject.Algorithms}</p>
                        `;
                        yearSection.appendChild(projectDiv);
                    }

                    // Display other projects after
                    otherProjects.forEach(project => {
                        const projectDiv = document.createElement('div');
                        projectDiv.className = 'project-card';
                        projectDiv.innerHTML = `
                            <h3>${project.Name}</h3>
                            <p><strong>Description:</strong> ${project.Description}</p>
                            <p><strong>Domain:</strong> ${project.Domain}</p>
                            <p><strong>Stakeholder:</strong> ${project.Stakeholder}</p>
                            <p><strong>Programming Languages:</strong> ${project["Programming Languages"]}</p>
                            <p><strong>Tools:</strong> ${project.Tools}</p>
                            <p><strong>Algorithms:</strong> ${project.Algorithms}</p>
                        `;
                        yearSection.appendChild(projectDiv);
                    });
                } else {
                    // For other years, display projects in original order
                    projectsByYear[year].forEach(project => {
                        const projectDiv = document.createElement('div');
                        projectDiv.className = 'project-card';
                        projectDiv.innerHTML = `
                            <h3>${project.Name}</h3>
                            <p><strong>Description:</strong> ${project.Description}</p>
                            <p><strong>Domain:</strong> ${project.Domain}</p>
                            <p><strong>Stakeholder:</strong> ${project.Stakeholder}</p>
                            <p><strong>Programming Languages:</strong> ${project["Programming Languages"]}</p>
                            <p><strong>Tools:</strong> ${project.Tools}</p>
                            <p><strong>Algorithms:</strong> ${project.Algorithms}</p>
                        `;
                        yearSection.appendChild(projectDiv);
                    });
                }

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