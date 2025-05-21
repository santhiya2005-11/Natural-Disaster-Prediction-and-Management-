import random
import matplotlib.pyplot as plt

# Step 1: Define regions and their base risk levels
regions = {
    "California": random.randint(5, 10),
    "Alaska": random.randint(6, 10),
    "Nevada": random.randint(4, 9),
    "Hawaii": random.randint(3, 8),
    "New York": random.randint(1, 4)
}

# Data for plotting
severity_data = {}
risk_levels = {}

# Step 2: Detect earthquake
def detect_earthquake(region):
    magnitude = round(random.uniform(3.0, 9.0), 1)
    print(f"\n[ALERT] Earthquake detected in {region}!")
    print(f"Magnitude: {magnitude}")
    assess_risk(region, magnitude)

# Step 3: Assess risk
def assess_risk(region, magnitude):
    base_risk = regions[region]
    severity = round(magnitude * base_risk / 10, 2)

    # Determine risk level
    if severity > 7:
        level = "High"
    elif severity > 4:
        level = "Moderate"
    else:
        level = "Low"

    print(f"Calculated Risk Level: {level}")
    severity_data[region] = severity
    risk_levels[region] = level
    manage_disaster(region, level)

# Step 4: Manage disaster
def manage_disaster(region, risk_level):
    print(f"\n[RESPONSE] Initiating response for {region}...")
    if risk_level == "High":
        print("-> Evacuate area, alert emergency services, prepare shelters.")
    elif risk_level == "Moderate":
        print("-> Issue public warnings, prepare emergency teams.")
    else:
        print("-> Monitor situation closely.")
    print("Response plan executed.\n")

# Step 5: Visualization
def plot_severity_chart():
    if not severity_data:
        print("No earthquakes detected, no chart to display.")
        return

    regions_list = list(severity_data.keys())
    severity_values = list(severity_data.values())
    colors = ['red' if risk_levels[region] == "High" else 
              'orange' if risk_levels[region] == "Moderate" else 'green'
              for region in regions_list]

    plt.figure(figsize=(10, 6))
    bars = plt.bar(regions_list, severity_values, color=colors)
    plt.title("Earthquake Severity by Region")
    plt.xlabel("Region")

    plt.figure(figsize=(10, 6))
    bars = plt.bar(regions_list, severity_values, color=colors)
    plt.title("Earthquake Severity by Region")
    plt.xlabel("Region")
    plt.ylabel("Severity Score")
    plt.ylim(0, 10)

    for bar, region in zip(bars, regions_list):
        plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.3,
                 f"{risk_levels[region]}", ha='center', color='black', fontsize=10)

    plt.grid(axis='y', linestyle='--', alpha=0.7)
    plt.tight_layout()
    plt.show()

# Step 6: Main function
def main():
    print("=== Natural Disaster Prediction and Management System ===")
    for region in regions:
        if random.random() < 0.5:  # 50% chance of earthquake
            detect_earthquake(region)
        else:
            print(f"\n[INFO] No earthquake activity detected in {region}.")

    plot_severity_chart()

if __name__ == "__main__":
    main()


