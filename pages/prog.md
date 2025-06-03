---
layout: default
---

# Project Repository

This section highlights projects done so far both in my accademic and professional life as a Statistician/Data Scientist, Teacher and recently Entrapreneur.

For now I've decided to group the project per Domain of application (<span style="color: #8b0000">Finance</span>, <span style="color: #006400">Insurance</span>, <span style="color: #ffa500">Retail</span>, <span style="color: #ff69b4">eCom</span>, <span style="color: #800080">Medical</span>, <span style="color: #8b4513">Edu</span>, <span style="color: #0000ff">Sport</span>).

In the chart, each project (`bubble`) is mapped into the date (`xaxis`) around which has been developed, the number of month it took to deliver (`size` of the bubble) and finally the recorded line of code I've manage to write for that project (`yaxis`).

<!-- Bubble Chart Container -->
<div id="bubble-chart" style="width: 100%; height: 500px; margin-bottom: 2em;"></div>

<script>
    // Wait for the DOM to be fully loaded
    document.addEventListener('DOMContentLoaded', function() {
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
                    margin: { t: 20, r: 20, b: 40, l: 60 },
                    xaxis: {
                        title: 'Year',
                        gridcolor: 'lightgray',
                        zerolinecolor: 'lightgray',
                        showgrid: false
                    },
                    yaxis: {
                        title: 'Lines of Code',
                        gridcolor: 'lightgray',
                        zerolinecolor: 'lightgray',
                        showgrid: false
                    },
                    hovermode: 'closest',
                    showlegend: false,
                    paper_bgcolor: 'rgba(0,0,0,0)',
                    plot_bgcolor: 'rgba(0,0,0,0)',
                    autosize: true
                };

                const config = {
                    responsive: true,
                    displayModeBar: false
                };

                Plotly.newPlot('bubble-chart', traces, layout, config);

                // Handle window resize
                window.addEventListener('resize', function() {
                    Plotly.Plots.resize('bubble-chart');
                });
            })
            .catch(error => console.error('Error loading chart data:', error));
    });
</script>

<div id="projects-container"></div>

<script>
    // Fetch and display projects
    fetch('/assets/data/Projects_v2.json')
        .then(response => response.json())
        .then(projects => {
            const container = document.getElementById('projects-container');
            
            // Define domain colors
            const domainColors = {
                'Finance': '#8b0000',
                'Insurance': '#006400',
                'Retail': '#ffa500',
                'eCommerce': '#ff69b4',
                'Medical Imaging': '#800080',
                'Education': '#8b4513',
                'Sport Analytics': '#0000ff'
            };
            
            // Group projects by domain
            const projectsByDomain = projects.reduce((acc, project) => {
                const domain = project.Domain;
                if (!acc[domain]) {
                    acc[domain] = [];
                }
                acc[domain].push(project);
                return acc;
            }, {});

            // Sort domains in a specific order (matching JSON keys)
            const domainOrder = ['Finance', 'Insurance', 'Retail', 'eCommerce', 'Medical Imaging', 'Education', 'Sport Analytics'];
            const sortedDomains = domainOrder.filter(domain => projectsByDomain[domain]);

            // Create HTML for each domain
            sortedDomains.forEach(domain => {
                const domainSection = document.createElement('div');
                domainSection.className = 'domain-section';
                domainSection.innerHTML = `<h2 style="color: ${domainColors[domain]}">${domain}</h2>`;

                // Sort projects within domain by year (newest first)
                const sortedProjects = projectsByDomain[domain].sort((a, b) => b.Year - a.Year);

                // Display projects
                sortedProjects.forEach(project => {
                    const projectDiv = document.createElement('div');
                    projectDiv.className = 'project-card';
                    projectDiv.innerHTML = `
                        <h3>${project.Name} (${project.Year})</h3>
                        <p><strong>Description:</strong> ${project.Description}</p>
                        <p><strong>Stakeholder:</strong> ${project.Stakeholder}</p>
                        <p><strong>Programming Languages:</strong> ${project["Programming Languages"]}</p>
                        <p><strong>Tools:</strong> ${project.Tools}</p>
                        <p><strong>Algorithms:</strong> ${project.Algorithms}</p>
                        <p><strong>Months:</strong> ${project.Months}</p>
                        <p><strong>Lines of Code:</strong> ${project["# Line of Code"]}</p>
                    `;
                    domainSection.appendChild(projectDiv);
                });

                container.appendChild(domainSection);
            });
        })
        .catch(error => console.error('Error loading projects:', error));
</script>

<style>
    h1 {
        font-weight: normal;
    }
    .domain-section {
        margin-bottom: 2em;
    }
    .domain-section h2 {
        font-weight: normal;
        margin-bottom: 1em;
        padding-bottom: 0.3em;
        border-bottom: 1px solid #eaecef;
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