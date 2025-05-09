---
layout: post
title: "The History of the Internet: From Arpanet to the World Wide Web"
subtitle: "The internet has become an integral part of our lives, connecting people across the world and changing the way we communicate, work, and access information."
date: 2023-03-02 23:45:13 -0400
background: '/assets/images/blog/internet.jpeg'
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Danish Travel Budget Visualizations</title>
  
  <!-- React and ReactDOM -->
  <script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>
  
  <!-- Recharts for radar chart -->
  <script src="https://unpkg.com/recharts@2.1.12/umd/Recharts.min.js" crossorigin></script>
  
  <!-- Babel for JSX -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  
  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #fafafa;
    }
    
    .container {
      max-width: 1000px;
      margin: 0 auto;
    }
    
    .chart-container {
      background-color: white;
      padding: 25px;
      margin-bottom: 30px;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }
    
    .chart-title {
      text-align: center;
      margin-bottom: 25px;
      color: #333;
      font-size: 20px;
      font-weight: bold;
    }
    
    .chart-subtitle {
      text-align: center;
      color: #666;
      font-size: 14px;
      margin-bottom: 20px;
    }
    
    .tabs {
      display: flex;
      justify-content: center;
      margin-bottom: 25px;
    }
    
    .tab-button {
      background: none;
      border: none;
      padding: 10px 20px;
      margin: 0 5px;
      cursor: pointer;
      border-radius: 20px;
      font-size: 14px;
      color: #666;
    }
    
    .tab-button.active {
      background-color: #f0f0f0;
      color: #333;
      font-weight: bold;
    }
    
    .tooltip {
      background-color: white;
      padding: 10px 15px;
      border-radius: 5px;
      box-shadow: 0 1px 5px rgba(0,0,0,0.15);
    }
    
    .tooltip-title {
      font-weight: bold;
      margin-bottom: 5px;
    }
    
    .tooltip-content {
      font-size: 14px;
    }
    
    .tooltip-label-purple {
      color: #8884d8;
    }
    
    .tooltip-label-green {
      color: #82ca9d;
    }
    
    .tooltip-label-yellow {
      color: #ffc658;
    }
    
    .tooltip-total {
      margin-top: 5px;
      font-weight: bold;
      border-top: 1px solid #eee;
      padding-top: 5px;
    }
    
    .hint {
      text-align: center;
      font-size: 13px;
      color: #888;
      margin-top: 10px;
    }
    
    .controls-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
    
    .sort-control {
      display: flex;
      align-items: center;
    }
    
    .sort-control label {
      margin-right: 8px;
      font-size: 14px;
      color: #666;
    }
    
    .sort-control select {
      padding: 6px 10px;
      border-radius: 4px;
      border: 1px solid #ddd;
      background-color: white;
      font-size: 14px;
      color: #333;
    }
    
    .highlight-hint {
      font-size: 13px;
      color: #888;
    }
    
    @media (max-width: 768px) {
      .chart-container {
        padding: 15px;
      }
      
      .tabs {
        flex-wrap: wrap;
      }
      
      .controls-row {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
      }
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    // Hardcoded data for all three datasets
    const datasets = {
      "socioeconomic": {
        "title": "Travel Budget by Socioeconomic Group",
        "data": [
          {
            "group": "Lønmodtager på højeste niveau",
            "translated": "High Income",
            "Rejsepakker": 7628,
            "Restauranter": 24289,
            "Overnatning": 9572
          },
          {
            "group": "Selvstændig",
            "translated": "Self-employed",
            "Rejsepakker": 4581,
            "Restauranter": 18340,
            "Overnatning": 10129
          },
          {
            "group": "Lønmodtager på mellemniveau",
            "translated": "Medium Income",
            "Rejsepakker": 6538,
            "Restauranter": 19945,
            "Overnatning": 5450
          },
          {
            "group": "Gennemsnitshusstand",
            "translated": "Average Household",
            "Rejsepakker": 4710,
            "Restauranter": 14197,
            "Overnatning": 5138
          },
          {
            "group": "Lønmodtager på grundniveau",
            "translated": "Basic Income",
            "Rejsepakker": 4413,
            "Restauranter": 16423,
            "Overnatning": 5677
          },
          {
            "group": "Arbejdsløs",
            "translated": "Unemployed",
            "Rejsepakker": 155,
            "Restauranter": 16515,
            "Overnatning": 11420
          },
          {
            "group": "Uddannelsessøgende",
            "translated": "Student",
            "Rejsepakker": 1673,
            "Restauranter": 11459,
            "Overnatning": 2294
          },
          {
            "group": "Pensionist, efterlønsmodtager",
            "translated": "Pensioner",
            "Rejsepakker": 4393,
            "Restauranter": 7323,
            "Overnatning": 2972
          },
          {
            "group": "Ude af erhverv i øvrigt",
            "translated": "Not in Workforce",
            "Rejsepakker": 1320,
            "Restauranter": 7367,
            "Overnatning": 2068
          }
        ]
      },
      "age": {
        "title": "Travel Budget by Age Group",
        "data": [
          {
            "group": "Average Household",
            "translated": "Average Household",
            "Rejsepakker": 4710,
            "Restauranter": 14197,
            "Overnatning": 5138
          },
          {
            "group": "Under 30 years",
            "translated": "Under 30 years",
            "Rejsepakker": 2676,
            "Restauranter": 15550,
            "Overnatning": 2229
          },
          {
            "group": "30–44 years",
            "translated": "30–44 years",
            "Rejsepakker": 3251,
            "Restauranter": 17611,
            "Overnatning": 5840
          },
          {
            "group": "45–59 years",
            "translated": "45–59 years",
            "Rejsepakker": 6265,
            "Restauranter": 17266,
            "Overnatning": 6973
          },
          {
            "group": "60–74 years",
            "translated": "60–74 years",
            "Rejsepakker": 5764,
            "Restauranter": 12677,
            "Overnatning": 6131
          },
          {
            "group": "75 years and older",
            "translated": "75 years and older",
            "Rejsepakker": 4135,
            "Restauranter": 6602,
            "Overnatning": 2140
          }
        ]
      },
      "region": {
        "title": "Travel Budget by Region",
        "data": [
          {
            "group": "Average Household",
            "translated": "Average Household",
            "Rejsepakker": 4710,
            "Restauranter": 14197,
            "Overnatning": 5138
          },
          {
            "group": "Capital Region",
            "translated": "Capital Region",
            "Rejsepakker": 5821,
            "Restauranter": 19082,
            "Overnatning": 7204
          },
          {
            "group": "Zealand Region",
            "translated": "Zealand Region",
            "Rejsepakker": 3874,
            "Restauranter": 11538,
            "Overnatning": 2929
          },
          {
            "group": "Southern Denmark",
            "translated": "Southern Denmark",
            "Rejsepakker": 3778,
            "Restauranter": 12133,
            "Overnatning": 3728
          },
          {
            "group": "Central Jutland",
            "translated": "Central Jutland",
            "Rejsepakker": 4628,
            "Restauranter": 12906,
            "Overnatning": 5763
          },
          {
            "group": "North Jutland",
            "translated": "North Jutland",
            "Rejsepakker": 4445,
            "Restauranter": 9569,
            "Overnatning": 3177
          }
        ]
      }
    };
    
    // Destructure Recharts components
    const {
      RadarChart, 
      PolarGrid, 
      PolarAngleAxis, 
      PolarRadiusAxis, 
      Radar, 
      Legend, 
      Tooltip, 
      ResponsiveContainer
    } = Recharts;
    
    // Custom tooltip component with percentages and totals
    const CustomTooltip = ({ active, payload, label }) => {
      if (active && payload && payload.length) {
        const data = payload[0].payload;
        
        // Calculate total spending
        const total = data.Rejsepakker + data.Restauranter + data.Overnatning;
        
        // Calculate percentages
        const packagePercent = Math.round((data.Rejsepakker / total) * 100);
        const restaurantPercent = Math.round((data.Restauranter / total) * 100);
        const accommodationPercent = Math.round((data.Overnatning / total) * 100);
        
        return (
          <div className="tooltip">
            <div className="tooltip-title">{data.translated}</div>
            <div className="tooltip-content">
              <div className="tooltip-label-purple">
                Rejsepakker: {data.Rejsepakker.toLocaleString()} DKK ({packagePercent}%)
              </div>
              <div className="tooltip-label-green">
                Restauranter: {data.Restauranter.toLocaleString()} DKK ({restaurantPercent}%)
              </div>
              <div className="tooltip-label-yellow">
                Overnatning: {data.Overnatning.toLocaleString()} DKK ({accommodationPercent}%)
              </div>
              <div className="tooltip-total">
                Total: {total.toLocaleString()} DKK
              </div>
            </div>
          </div>
        );
      }
      return null;
    };
    
    const App = () => {
      // State to track which dataset is active
      const [activeDataset, setActiveDataset] = React.useState('socioeconomic');
      
      // State to track highlighted category
      const [activeCategory, setActiveCategory] = React.useState(null);
      
      // State for sorting
      const [sortBy, setSortBy] = React.useState('default');
      
      // Get available datasets
      const availableDatasets = Object.keys(datasets);
      
      // Format display names
      const displayNames = {
        'socioeconomic': 'Socioeconomic Groups',
        'age': 'Age Groups',
        'region': 'Regions'
      };
      
      // Sort the data based on the sort selection
      const sortedData = React.useMemo(() => {
        if (sortBy === 'default') return datasets[activeDataset].data;
        
        return [...datasets[activeDataset].data].sort((a, b) => {
          if (sortBy === 'total') {
            const totalA = a.Rejsepakker + a.Restauranter + a.Overnatning;
            const totalB = b.Rejsepakker + b.Restauranter + b.Overnatning;
            return totalB - totalA; // Descending
          }
          return b[sortBy] - a[sortBy]; // Descending by category
        });
      }, [activeDataset, sortBy, datasets]);
      
      // Handle legend click to toggle category highlight
      const handleLegendClick = (entry) => {
        if (activeCategory === entry.dataKey) {
          setActiveCategory(null); // Deselect if already selected
        } else {
          setActiveCategory(entry.dataKey); // Select the clicked category
        }
      };
      
      return (
        <div className="container">
          <h1 className="chart-title">Danish Travel Budget Analysis</h1>
          
          {/* Dataset tabs */}
          <div className="tabs">
            {availableDatasets.map(key => (
              <button 
                key={key}
                className={`tab-button ${activeDataset === key ? 'active' : ''}`}
                onClick={() => setActiveDataset(key)}
              >
                {displayNames[key]}
              </button>
            ))}
          </div>
          
          <div className="chart-container">
            <div className="chart-title">{datasets[activeDataset].title}</div>
            
            {/* Controls row with sorting */}
            <div className="controls-row">
              <div className="chart-subtitle">Travel expenses in DKK</div>
              
              <div className="sort-control">
                <label htmlFor="sort-select">Sort by:</label>
                <select 
                  id="sort-select"
                  value={sortBy}
                  onChange={(e) => setSortBy(e.target.value)}
                >
                  <option value="default">Default Order</option>
                  <option value="total">Total Spending</option>
                  <option value="Rejsepakker">Travel Packages</option>
                  <option value="Restauranter">Restaurants</option>
                  <option value="Overnatning">Accommodation</option>
                </select>
              </div>
            </div>
            
            <ResponsiveContainer width="100%" height={500}>
              <RadarChart outerRadius={150} data={sortedData}>
                <PolarGrid stroke="#e5e5e5" />
                <PolarAngleAxis dataKey="translated" tick={{ fontSize: 12, fill: '#666' }} />
                <PolarRadiusAxis tick={false} axisLine={false} />
                
                <Radar 
                  name="Rejsepakker" 
                  dataKey="Rejsepakker" 
                  stroke="#8884d8" 
                  fill="#8884d8" 
                  fillOpacity={activeCategory === null || activeCategory === "Rejsepakker" ? 0.6 : 0.2}
                  activeDot={{ r: 5 }}
                />
                <Radar 
                  name="Restauranter" 
                  dataKey="Restauranter" 
                  stroke="#82ca9d" 
                  fill="#82ca9d" 
                  fillOpacity={activeCategory === null || activeCategory === "Restauranter" ? 0.6 : 0.2}
                  activeDot={{ r: 5 }}
                />
                <Radar 
                  name="Overnatning" 
                  dataKey="Overnatning" 
                  stroke="#ffc658" 
                  fill="#ffc658" 
                  fillOpacity={activeCategory === null || activeCategory === "Overnatning" ? 0.6 : 0.2}
                  activeDot={{ r: 5 }}
                />
                
                <Tooltip content={<CustomTooltip />} />
                <Legend 
                  onClick={(entry) => handleLegendClick(entry)}
                  formatter={(value, entry) => {
                    // Highlight active category in legend
                    const isActive = activeCategory === entry.dataKey || !activeCategory;
                    return <span style={{color: isActive ? entry.color : '#999', fontWeight: isActive ? 'bold' : 'normal'}}>{value}</span>;
                  }}
                />
              </RadarChart>
            </ResponsiveContainer>
            
            <div className="hint">
              <div><strong>Interactive features:</strong></div>
              <div>• Click on legend items to highlight specific categories</div>
              <div>• Hover over points to see detailed values</div>
              <div>• Use the sort dropdown to reorder the data</div>
            </div>
          </div>
        </div>
      );
    };
    
    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>