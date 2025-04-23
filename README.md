INPUT 

% Motor Sizing for Electric Vehicle
% This program calculates the required motor power and peak power
% based on the forces acting on the vehicle.
 
% Input Parameters
kerb_weight_kg = 1500; % Vehicle's kerb weight in kg
payload_kg = 200; % Payload in kg
drag_coefficient = 0.3; % Air drag coefficient
rolling_resistance_coefficient = 0.015; % Coefficient of rolling resistance
tyre_radius_m = 0.33; % Tyre radius in meters
target_speed_kmph = 72; % Target speed in km/h
incline_angle_deg = 5; % Incline angle in degrees
frontal_area_m2 = 2.5; % Frontal area of vehicle in square meters
air_density_kg_m3 = 1.225; % Air density in kg/m^3
 
% Conversions and Constants
target_speed_mps = target_speed_kmph / 3.6; % Convert speed to m/s
total_weight_N = (kerb_weight_kg + payload_kg) * 9.81; % Total weight in Newtons
 
% Force Calculations
rolling_resistance = rolling_resistance_coefficient * total_weight_N; % Rolling resistance force
air_drag_force = 0.5 * drag_coefficient * air_density_kg_m3 * frontal_area_m2 * target_speed_mps^2; % Air drag force
incline_angle_rad = deg2rad(incline_angle_deg); % Convert incline angle to radians
hill_climbing_force = total_weight_N * sin(incline_angle_rad); % Hill climbing force
 
% Total Tractive Force
total_tractive_force = rolling_resistance + air_drag_force + hill_climbing_force;
 
% Motor Power Calculations
motor_power_watts = total_tractive_force * target_speed_mps; % Motor power in Watts
peak_power_watts = motor_power_watts * 1.2; % Peak power with 20% safety margin
 
% Display Results
fprintf('--- Electric Vehicle Motor Sizing ---\n');
fprintf('Rolling Resistance Force: %.2f N\n', rolling_resistance);
fprintf('Air Drag Force: %.2f N\n', air_drag_force);
fprintf('Hill Climbing Force: %.2f N\n', hill_climbing_force);
fprintf('Total Tractive Force: %.2f N\n', total_tractive_force);
fprintf('Motor Power Required: %.2f Watts\n', motor_power_watts);
fprintf('Peak Motor Power: %.2f Watts\n', peak_power_watts);
fprintf('-------------------------------------\n');

