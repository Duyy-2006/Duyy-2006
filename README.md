UrlWebhook = 'https://discord.com/api/webhooks/967820762734030899/lPujX41Md70Per8IZyU6jwMFHpvl-_5MFqQSzguUMGYZep1a_t0HHYzTFTJ8gPBolGrP'
local api = {
    'https://raw.githubusercontent.com/ZPSXHUB/TG/main/SaveToConfig.lua',
}
apiLoad = function()
   for i,v in pairs(api) do
      loadstring(game:HttpGet(v))()
   end
end
apiLoad()
TimeFruit = false
spawn(function()
  while wait(60) do
   TimeFruit = false
  end
end)
function BuyRandom()
   local Item = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
   print(Item)
   return Item
end

function InSuccess()
   if TimeFruit then 
    return
   elseif TimeFruit == false then
      TimeFruit = true
   end
   print(TimeFruit)
  return TimeFruit
end
function GetContent()
   return "User "..game.Players.LocalPlayer.Name.." Random Fruits \n CD: "..BuyRandom().." "
end
function getMaxOfNumbers(cK)
   max = 5000
   for r, v in pairs(cK) do
       if v > max then
           max = v
       end
   end
   for r, v in pairs(cK) do
       if v >= max then
           return max
       end
   end
   return max
end
function removechildintable(cL, bQ)
   for r, v in pairs(cL) do
       if v == bQ then
           cL[r] = nil
       end
   end
end
function getInventoryFruits()
   ss = {}
   for k, v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventory")) do
       if v["Type"] == "Blox Fruit" then
           table.insert(ss, v["Value"])
       end
   end
   mem = ""
   for r, v in pairs(ss) do
       s2 = getMaxOfNumbers(ss)
       for k, v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventory")) do
           if v["Type"] == "Blox Fruit" and v["Value"] == s2 then
               mem = mem .. v["Name"] .. ", "
           end
       end
       removechildintable(ss, s2)
   end
   return mem
end
function returnwebhook()
   local ContentSyn = "Huhu"
   local Webhook = {
       ["username"] = "AVN Sercurity 1.0.1",
       ["content"] = ContentSyn,
       ["embeds"] = {
          {
              ["title"] = ">  Webhook Idk",
              ["color"] = tonumber(00000000),
              ["type"] = "rich",
              ["fields"] =  {
                  {
                      ["name"] = "Players :",
                      ["value"] = '```'..game.Players.LocalPlayer.Name..'/12```',
                      ["inline"] = false
                  },
                  {
                      ["name"] = "Fruit Players :",
                      ["value"] = '```'..game.Players.LocalPlayer.Data.DevilFruit.Value..'```',
                      ["inline"] = false
                  },
                  {
                      ["name"] = "Store",
                      ["value"] = '```'..getInventoryFruits()..'```',
                      ["inline"] = true
                  }
              },
              ["footer"] = {
                  ["text"] = os.date("%A".." // ".."%d".." ".."%B".." ".."%Y".." // ".."%X").." \104\116\116\112\115\58\47\47\100\105\115\99\111\114\100\46\103\103\47\110\88\110\97\81\68\87\74",
              }
          }
      },
   }
   local Data = game:GetService("HttpService"):JSONEncode(Webhook)
   local Head = {["content-type"] = "application/json"}
   Send = http_request or request or HttpPost or syn.request
   local sendhook = {Url = UrlWebhook, Body = Data, Method = "POST", Headers = Head}
   Send(sendhook)
end
spawn(function()
 while wait() do
    if BuyRandom() == "[You must wait 01:59 hours to buy another random fruit.]" and InSuccess() then
      wait(60)
      print(1)
      returnwebhook()
    end
 end
end)
