-- UI Fly avec vitesse personnalisable

-- Variables
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local mouse = LocalPlayer:GetMouse()
local flying = false
local speed = 50

-- UI Setup
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 200, 0, 150)
Frame.Position = UDim2.new(0, 100, 0, 100)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.BorderSizePixel = 0
Frame.Active = true
Frame.Draggable = true

-- Slider label
local Label = Instance.new("TextLabel", Frame)
Label.Size = UDim2.new(1, 0, 0, 25)
Label.Position = UDim2.new(0, 0, 0, 0)
Label.Text = "Vitesse: " .. speed
Label.TextColor3 = Color3.new(1, 1, 1)
Label.BackgroundTransparency = 1

-- Slider
local Slider = Instance.new("TextBox", Frame)
Slider.Size = UDim2.new(1, -20, 0, 25)
Slider.Position = UDim2.new(0, 10, 0, 30)
Slider.Text = tostring(speed)
Slider.TextColor3 = Color3.new(1, 1, 1)
Slider.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Slider.ClearTextOnFocus = false

-- Toggle Button
local Toggle = Instance.new("TextButton", Frame)
Toggle.Size = UDim2.new(1, -20, 0, 30)
Toggle.Position = UDim2.new(0, 10, 0, 70)
Toggle.Text = "Fly: OFF"
Toggle.TextColor3 = Color3.new(1, 1, 1)
Toggle.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

-- Fly function
local BodyGyro = Instance.new("BodyGyro")
local BodyVelocity = Instance.new("BodyVelocity")

function startFly()
	local char = LocalPlayer.Character
	local hrp = char:WaitForChild("HumanoidRootPart")
	BodyGyro.Parent = hrp
	BodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
	BodyGyro.P = 9e4
	BodyGyro.CFrame = hrp.CFrame

	BodyVelocity.Parent = hrp
	BodyVelocity.Velocity = Vector3.new(0, 0, 0)
	BodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)

	game:GetService("RunService").RenderStepped:Connect(function()
		if flying then
			local cf = workspace.CurrentCamera.CFrame
			local direction = Vector3.new()

			if mouse.W then direction += cf.LookVector end
			if mouse.S then direction -= cf.LookVector end
			if mouse.A then direction -= cf.RightVector end
			if mouse.D then direction += cf.RightVector end

			BodyVelocity.Velocity = direction.Unit * speed + Vector3.new(0, 1, 0)
			BodyGyro.CFrame = workspace.CurrentCamera.CFrame
		end
	end)
end

-- Button action
Toggle.MouseButton1Click:Connect(function()
	flying = not flying
	Toggle.Text = "Fly: " .. (flying and "ON" or "OFF")
	if flying then
		startFly()
	else
		BodyGyro:Destroy()
		BodyVelocity:Destroy()
	end
end)

-- Slider action
Slider.FocusLost:Connect(function()
	local val = tonumber(Slider.Text)
	if val then
		speed = val
		Label.Text = "Vitesse: " .. speed
	end
end)
