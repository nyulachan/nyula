--[[ INFORMATION
    Combination of BitchBot and BeanBot's ESPs.
    I honestly have no idea what I did anymore i think it was that i decluttered code and shizzle

    BTW THIS IS SUPPOSED TO BE UNOBFUSCATED I ADMIT MOST OF THIS AINT MY CODE ( i am uninterested in actually making an ESP cus nobody uses them in "hood" games, this was just to have something a bit more customizale than kiriot's esp )
]]

--[[ Default Config 

_G.ESPSettings = {
    enabled = false,
	box = false,
	boxcolor1 = Color3.fromRGB(255,255,255),
	name = false,
	displayname = false,
	headdot = false,
	health = false,
    healthcolor = Color3.fromRGB(255,255,255),
    healthtransparency = 1,
	healthbar = false,
	healthbarcolor1 = Color3.fromRGB(0,255,0),
	healthbarcolor2 = Color3.fromRGB(255,0,0),
	distance = false,
	outoffovarrows = false,
	arrowsoffset = 10,
	arrowscolor = Color3.fromRGB(255,255,255),
    arrowsfilled = false,
    arrowsthickness = 2.5,
	textcase = 1,
	maxtextlength = 2^16,
	hpvisibilitycap = 100,
	checks = {
        false, -- alive check ( not down check just alive check ? )
        false, -- distance check 
	},
    maxdistance = 2^16,
}

]]
if not _G.ESPSettings then
    game.Players.LocalPlayer:Kick("Missing _G.ESPSettings config")
    return
end
if _G.ESPLoaded then return end -- makes it so u cant execute the ACTUAL esp twice, itll just change config on 2nd and so on executions
_G.ESPLoaded = true
LPH_JIT_MAX = function(...) return ... end -- if u wanna obfuscate this then this makes stuff faster if ur using luraph (is just a normal function when not obfuscated with luraph)
local CreateESP={}
local RGB = Color3.fromRGB
function CreateESP:FilledRect(visible, pos_x, pos_y, width, height, clr, tablename)
    local temptable = Drawing.new("Square")
    temptable.Visible = visible
    temptable.Position = Vector2.new(pos_x, pos_y)
    temptable.Size = Vector2.new(width, height)
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    temptable.Filled = true
    temptable.Thickness = 0
    temptable.Transparency = clr[4] / 255
    table.insert(tablename, temptable)
end
function CreateESP:Circle(visible, pos_x, pos_y, size, thickness, sides, clr, tablename)
    local temptable = Drawing.new("Circle")
    temptable.Position = Vector2.new(pos_x, pos_y)
    temptable.Visible = visible
    temptable.Radius = size
    temptable.Thickness = thickness
    temptable.NumSides = sides
    temptable.Transparency = clr[4]
    temptable.Filled = false
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    table.insert(tablename, temptable)
end
function CreateESP:OutlinedRect(visible, pos_x, pos_y, width, height, clr, tablename)
    local temptable = Drawing.new("Square")
    temptable.Visible = visible
    temptable.Position = Vector2.new(pos_x, pos_y)
    temptable.Size = Vector2.new(width, height)
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    temptable.Filled = false
    temptable.Thickness = 0
    temptable.Transparency = clr[4] / 255
    table.insert(tablename, temptable)
end
function CreateESP:FilledRect(visible, pos_x, pos_y, width, height, clr, tablename)
    local temptable = Drawing.new("Square")
    temptable.Visible = visible
    temptable.Position = Vector2.new(pos_x, pos_y)
    temptable.Size = Vector2.new(width, height)
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    temptable.Filled = true
    temptable.Thickness = 0
    temptable.Transparency = clr[4] / 255
    table.insert(tablename, temptable)
end
function CreateESP:OutlinedText(text, font, visible, pos_x, pos_y, size, centered, clr, clr2, tablename)
    local temptable = Drawing.new("Text")
    temptable.Text = text
    temptable.Visible = visible
    temptable.Position = Vector2.new(pos_x, pos_y)
    temptable.Size = size
    temptable.Center = centered
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    temptable.Transparency = clr[4] / 255
    temptable.Outline = true
    temptable.OutlineColor = RGB(clr2[1], clr2[2], clr2[3])
    temptable.Font = font
    if tablename then
        table.insert(tablename, temptable)
    end
    return temptable
end
function CreateESP:Triangle(visible,placeholder,placeholder2,thickness,placeholder3,clr,tablename)
    local temptable = Drawing.new("Triangle")
    temptable.Visible = visible
    temptable.Thickness = thickness
    temptable.Color = RGB(clr[1], clr[2], clr[3])
    if tablename then
        table.insert(tablename, temptable)
    end
    return temptable
end

local loadedESPStuff = {headdotoutline = {},headdot = {},name = {},displayname = {},box = {},filledbox = {},innerbox = {},healthouter = {},healthinner = {},hptext = {},distance = {},arrows = {},}
for i=1,game.Players.MaxPlayers do -- smart as hell ngl like shii already make the amount of items for the shit u need
    CreateESP:FilledRect(false, 20, 20, 20, 20, { 0, 0, 0, 220 }, loadedESPStuff.filledbox)
	CreateESP:Circle(false, 20, 20, 10, 3, 10, { 10, 10, 10, 215 }, loadedESPStuff.headdotoutline)
	CreateESP:Circle(false, 20, 20, 10, 1, 10, { 255, 255, 255, 255 }, loadedESPStuff.headdot)
	CreateESP:OutlinedRect(false, 20, 20, 20, 20, { 0, 0, 0, 220 }, loadedESPStuff.innerbox)
	CreateESP:OutlinedRect(false, 20, 20, 20, 20, { 255, 255, 255, 255 }, loadedESPStuff.box)
	CreateESP:FilledRect(false, 20, 20, 4, 20, { 10, 10, 10, 215 }, loadedESPStuff.healthouter)
	CreateESP:FilledRect(false, 20, 20, 20, 20, { 255, 255, 255, 255 }, loadedESPStuff.healthinner)
	CreateESP:OutlinedText("", 1, false, 20, 20, 13, false, { 255, 255, 255, 255 }, { 0, 0, 0 }, loadedESPStuff.hptext)
	CreateESP:OutlinedText("", 2, false, 20, 20, 13, true, { 255, 255, 255, 255 }, { 0, 0, 0 }, loadedESPStuff.distance)
	CreateESP:OutlinedText("", 2, false, 20, 20, 13, true, { 255, 255, 255, 255 }, { 0, 0, 0 }, loadedESPStuff.name)
	CreateESP:OutlinedText("", 2, false, 20, 20, 13, true, { 255, 255, 255, 255 }, { 0, 0, 0 }, loadedESPStuff.displayname)
	CreateESP:OutlinedText("", 2, false, 20, 20, 13, true, { 255, 255, 255, 255 }, { 0, 0, 0 }, loadedESPStuff.team)
    CreateESP:Triangle(false, 20, 20, 2.4, false, { 255, 255, 255, 255 }, loadedESPStuff.arrows)
end
local Players = game.Players
local LOCAL_PLAYER = game.Players.LocalPlayer
-- next 2 functions are actually mad annoying 

function string_cut(s1, num)
	return num == 0 and s1 or string.sub(s1, 1, num)
end
function formattext(text)
    if _G.ESPSettings.textcase == 1 then
        return string_cut(string.lower(text), _G.ESPSettings.maxtextlength)
    elseif _G.ESPSettings.textcase == 3 then
        return string_cut(string.upper(text), _G.ESPSettings.maxtextlength)
    end
    return string_cut(text, _G.ESPSettings.maxtextlength)
end
game:GetService("RunService").RenderStepped:Connect(LPH_JIT_MAX(function()
    for k, v in pairs(loadedESPStuff) do
        for k1, v1 in ipairs(v) do
            if v1.Visible then
                v1.Visible = false
            end
        end
    end
    local organizedPlayers = {}
    for i, v in ipairs(Players:GetPlayers()) do
        local checks = _G.ESPSettings.checks
        if v and v.Character and v.Character:FindFirstChild("Humanoid") then
            local humanoid = v.Character:FindFirstChild("Humanoid")
            if _G.ESPSettings.enabled and v.Character ~= nil and v.Character:FindFirstChild("HumanoidRootPart") and not (v==LOCAL_PLAYER) and not (checks[1] and humanoid.Health <= 0) and not (checks[2] and LOCAL_PLAYER:DistanceFromCharacter(v.Character.HumanoidRootPart.Position) / 5 > _G.ESPSettings.maxdistance) then
                table.insert(organizedPlayers, v)
            end 
        end
    end
    local textcase = _G.ESPSettings.textcase
    local textlength = _G.ESPSettings.maxtextlength
    for i, v in ipairs(organizedPlayers) do
        pcall(function() -- pcall ignores errors (makes them not print into synx console)
            local humanoid = v.Character:FindFirstChild("Humanoid")
            local rootpart = v.Character.HumanoidRootPart.Position
            local cam = workspace.CurrentCamera.CFrame
            local torso = v.Character.PrimaryPart.CFrame
            local head = v.Character.Head.CFrame
            local top, top_isrendered = workspace.CurrentCamera:WorldToViewportPoint(head.Position + (torso.UpVector * 1) + cam.UpVector)
            local bottom, bottom_isrendered = workspace.CurrentCamera:WorldToViewportPoint(torso.Position - (torso.UpVector * 2.5) - cam.UpVector)
            local minY = math.abs(bottom.y - top.y)
            local sizeX = math.ceil(math.max(math.clamp(math.abs(bottom.x - top.x) * 2.5, 0, minY), minY / 2, 3))
            local sizeY = math.ceil(math.max(minY, sizeX * 0.5, 3))
            if top_isrendered or bottom_isrendered then
                local boxtop = Vector2.new(
                    math.floor(top.x * 0.5 + bottom.x * 0.5 - sizeX * 0.5),
                    math.floor(math.min(top.y, bottom.y))
                )
                local boxsize = { w = sizeX, h = sizeY }

                if _G.ESPSettings.headdot then
                    local head = v.Character:FindFirstChild("Head")
                    if head then
                        local headpos = head.Position
                        local headdotpos = workspace.CurrentCamera:WorldToViewportPoint(Vector3.new(headpos.x, headpos.y + 0.1, headpos.z))
                        local headdotpos_b = workspace.CurrentCamera:WorldToViewportPoint(Vector3.new(headpos.x, headpos.y - 0.2, headpos.z))
                        local difference = headdotpos_b.y - headdotpos.y
                        loadedESPStuff.headdot[i].Visible = true
                        loadedESPStuff.headdot[i].Position = Vector2.new(headdotpos.x, headdotpos_b.y - difference)
                        loadedESPStuff.headdot[i].Radius = difference * 2

                        loadedESPStuff.headdotoutline[i].Visible = true
                        loadedESPStuff.headdotoutline[i].Position = Vector2.new(headdotpos.x, headdotpos_b.y - difference)
                        loadedESPStuff.headdotoutline[i].Radius = difference * 2
                    end
                end
                if _G.ESPSettings.box then
                    loadedESPStuff.innerbox[i].Position = Vector2.new(boxtop.x + 1, boxtop.y + 1)
                    loadedESPStuff.innerbox[i].Size = Vector2.new(boxsize.w - 2, boxsize.h - 2)
                    loadedESPStuff.innerbox[i].Visible = true
                    loadedESPStuff.innerbox[i].Color = _G.ESPSettings.boxcolor1

                    loadedESPStuff.box[i].Position = Vector2.new(boxtop.x, boxtop.y)
                    loadedESPStuff.box[i].Size = Vector2.new(boxsize.w, boxsize.h)
                    loadedESPStuff.box[i].Visible = true
                    loadedESPStuff.box[i].Color = _G.ESPSettings.boxcolor1
                end
                if humanoid then
                    local health = math.ceil(humanoid.Health)
                    local maxhealth = humanoid.MaxHealth
                    local Lerp = function(delta, from, to)
                        if (delta > 1) then
                            return to
                        end
                        if (delta < 0) then
                            return from
                        end
                        return from + (to - from) * delta
                    end
                    local ColorRange = function(value, ranges) -- "tony" made this idk who that is but its in whichever esp it came from
                        if value <= ranges[1].start then
                            return ranges[1].color
                        end
                        if value >= ranges[#ranges].start then
                            return ranges[#ranges].color
                        end
                    
                        local selected = #ranges
                        for i = 1, #ranges - 1 do
                            if value < ranges[i + 1].start then
                                selected = i
                                break
                            end
                        end
                        local minColor = ranges[selected]
                        local maxColor = ranges[selected + 1]
                        local lerpValue = (value - minColor.start) / (maxColor.start - minColor.start)
                        return Color3.new(
                            Lerp(lerpValue, minColor.color.r, maxColor.color.r),
                            Lerp(lerpValue, minColor.color.g, maxColor.color.g),
                            Lerp(lerpValue, minColor.color.b, maxColor.color.b)
                        )
                    end
                    if _G.ESPSettings.healthbar then
                        loadedESPStuff.healthouter[i].Position = Vector2.new(boxtop.x - 6, boxtop.y - 1)
                        loadedESPStuff.healthouter[i].Size = Vector2.new(4, boxsize.h + 2)
                        loadedESPStuff.healthouter[i].Visible = true

                        local ySizeBar = -math.floor(boxsize.h * health / maxhealth)

                        loadedESPStuff.healthinner[i].Position = Vector2.new(boxtop.x - 5, boxtop.y + boxsize.h)
                        loadedESPStuff.healthinner[i].Size = Vector2.new(2, ySizeBar)
                        loadedESPStuff.healthinner[i].Visible = true
                        loadedESPStuff.healthinner[i].Color = ColorRange(health, {
                            [1] = {
                                start = 0,
                                color = _G.ESPSettings.healthbarcolor2,
                            },
                            [2] = {
                                start = 100,
                                color = _G.ESPSettings.healthbarcolor1,
                            },
                        })

                        if _G.ESPSettings.health and _G.ESPSettings.hpvisibilitycap >= math.ceil((health / maxhealth) * 100) then
                            loadedESPStuff.hptext[i].Text = tostring(health)
                            local textsize = loadedESPStuff.hptext[i].TextBounds
                            loadedESPStuff.hptext[i].Position = Vector2.new(
                                boxtop.x - 7 - textsize.x,
                                boxtop.y + math.clamp(boxsize.h + ySizeBar - 8, -4, boxsize.h - 10)
                            )
                            loadedESPStuff.hptext[i].Visible = true
                            loadedESPStuff.hptext[i].Color = _G.ESPSettings.healthcolor
                            loadedESPStuff.hptext[i].Transparency = _G.ESPSettings.healthtransparency
                        end
                    elseif _G.ESPSettings.health and _G.ESPSettings.hpvisibilitycap >= math.ceil((health / maxhealth) * 100) then
                        loadedESPStuff.hptext[i].Text = tostring(health)
                        local textsize = loadedESPStuff.hptext[i].TextBounds
                        loadedESPStuff.hptext[i].Position = Vector2.new(boxtop.x - 3 - textsize.x, boxtop.y - 4)
                        loadedESPStuff.hptext[i].Visible = true
                        loadedESPStuff.hptext[i].Color = _G.ESPSettings.healthcolor
                        loadedESPStuff.hptext[i].Transparency = _G.ESPSettings.healthtransparency
                    end
                end
                if _G.ESPSettings.name then
                    loadedESPStuff.name[i].Text = formattext(v.Name)
                    loadedESPStuff.name[i].Position = (_G.ESPSettings.displayname and v.Name ~= v.DisplayName) and Vector2.new(math.floor(boxtop.x + boxsize.w * 0.5), math.floor(boxtop.y - 27)) or Vector2.new(math.floor(boxtop.x + boxsize.w * 0.5), math.floor(boxtop.y - 15))
                    loadedESPStuff.name[i].Visible = true
                end
                if _G.ESPSettings.displayname then
                    if _G.ESPSettings.name and v.Name ~= v.DisplayName then
                        loadedESPStuff.displayname[i].Text = formattext(v.DisplayName)
                        loadedESPStuff.displayname[i].Position = Vector2.new(math.floor(boxtop.x + boxsize.w * 0.5), math.floor(boxtop.y - 15))
                        loadedESPStuff.displayname[i].Visible = true
                    else 
                        loadedESPStuff.displayname[i].Text = formattext(v.DisplayName)
                        loadedESPStuff.displayname[i].Position = Vector2.new(math.floor(boxtop.x + boxsize.w * 0.5), math.floor(boxtop.y - 15))
                        loadedESPStuff.displayname[i].Visible = true
                    end
                end
                local y_spot = 0
                if _G.ESPSettings.distance then
                    local dist_pos = Vector2.new(math.floor(boxtop.x + boxsize.w * 0.5), boxtop.y + boxsize.h + y_spot)
                    loadedESPStuff.distance[i].Text = tostring(math.ceil(LOCAL_PLAYER:DistanceFromCharacter(rootpart) / 5)).. "m"
                    loadedESPStuff.distance[i].Position = dist_pos
                    loadedESPStuff.distance[i].Visible = true
                end
            else
                if _G.ESPSettings.outoffovarrows then
                    loadedESPStuff.arrows[i].Visible = true

                    local rel = workspace.CurrentCamera.CFrame:PointToObjectSpace(v.Character.HumanoidRootPart.Position)
                    local angle = math.atan2(-rel.Y, rel.X)

                    local dir = Vector2.new(math.cos(angle), math.sin(angle))

                    function ScreenSize()
                        return workspace.CurrentCamera.ViewportSize
                    end
                    function getRotate(v, rads)
                        local u = v.Unit
                        local a, b = math.sin(rads), math.cos(rads)
                        local c, d = (b * u.X) - (a * u.Y), (a * u.X) + (b * u.Y)
                        return Vector2.new(c, d).Unit * v.Magnitude
                    end
                    local pos = (dir * ScreenSize() * (_G.ESPSettings.arrowsoffset / 100)) + (ScreenSize() / 2)

                    local size = math.floor(ScreenSize().X / 64)

                    loadedESPStuff.arrows[i].PointA = pos
                    loadedESPStuff.arrows[i].PointB = pos - getRotate(dir, .5) * size
                    loadedESPStuff.arrows[i].PointC = pos - getRotate(dir, -.5) * size

                    loadedESPStuff.arrows[i].Color = _G.ESPSettings.arrowscolor
                    loadedESPStuff.arrows[i].Filled = _G.ESPSettings.arrowsfilled
                    loadedESPStuff.arrows[i].Thickness = _G.ESPSettings.arrowsthickness
                end
            end	
        end)
    end
end))
