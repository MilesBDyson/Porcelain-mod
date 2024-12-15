
-- translation support

local S = minetest.get_translator("porcelain")

-- list of mixture colors

local mixture = {
	{"natural", S("Natural")},
	{"white", S("White")},
	{"grey", S("Grey")},
	{"black", S("Black")},
	{"red", S("Red")},
	{"yellow", S("Yellow")},
	{"green", S("Green")},
	{"cyan", S("Cyan")},
	{"blue", S("Blue")},
	{"magenta", S("Magenta")},
	{"orange", S("Orange")},
	{"violet", S("Violet")},
	{"brown", S("Brown")},
	{"pink", S("Pink")},
	{"dark_grey", S("Dark Grey")},
	{"dark_green", S("Dark Green")}
}

-- check mod support
local farming_mod = minetest.get_modpath("farming")
local techcnc_mod = minetest.get_modpath("technic_cnc")
local stairs_mod = minetest.get_modpath("stairs")
local stairsplus_mod = minetest.get_modpath("moreblocks")
		and minetest.global_exists("stairsplus")
local stairsplus_compat = minetest.settings:get_bool("stairsplus_mixture_compatibility") ~= false


	-- register porcelain recipe
		minetest.register_craft({
			type = "cooking",
			output = "porcelain:natural",
			recipe = "porcelain:cold_mixture_natural"
		})

-- scroll through colours
for _, mixture in pairs(mixture) do

	-- register cold node
	minetest.register_node("porcelain:cold_mixture_" .. mixture[1], {
		description = mixture[2] .. " " .. S("Cold Mixture"),
		tiles = {"cold_mixture_" .. mixture[1] ..".png"},
		groups = {cracky = 3, porcelain = 1},
		sounds = default.node_sound_stone_defaults(),
		is_ground_content = false
	})
	
	-- register fired node
	minetest.register_node("porcelain:" .. mixture[1], {
		description = mixture[2] .. " " .. S("Porcelain"),
		tiles = {"porcelain_" .. mixture[1] ..".png"},
		groups = {cracky = 1, porcelain = 1},
		sounds = default.node_sound_stone_defaults(),
		is_ground_content = false
	})

	-- register fired recipe
	if mixture[1] ~= "natural" then
		minetest.register_craft({
			type = "cooking",
			output = "porcelain:" .. mixture[1],
			recipe = "porcelain:cold_mixture_" .. mixture[1]
		})
	end
	
	-- register cold mix recipe
	if mixture[1] ~= "natural" then
		minetest.register_craft({
			output = "porcelain:cold_mixture_" .. mixture[1] .. " 9",
			recipe = {
				{"porcelain:cold_mixture_natural", "porcelain:cold_mixture_natural", "porcelain:cold_mixture_natural"},
				{"porcelain:cold_mixture_natural", "dye:".. mixture[1], "porcelain:cold_mixture_natural"},
				{"porcelain:cold_mixture_natural", "porcelain:cold_mixture_natural", "porcelain:cold_mixture_natural"}
			}
		})
	end

	-- Porcelain
	-- stairs plus
	if stairsplus_mod then
		stairsplus:register_all("porcelain", "porcelain_" .. mixture[1],
				"porcelain:" .. mixture[1], {
			description = mixture[2] .. " " .. S("porcelain"),
			tiles = {"porcelain_" .. mixture[1] .. ".png"},
			groups = {cracky = 3},
			sounds = default.node_sound_stone_defaults()
		})
		if stairsplus_compat then
			stairsplus:register_alias_all("porcelain_", mixture[1],
					"porcelain_", "porcelain_" .. mixture[1])
			minetest.register_alias("stairs:slab_porcelain_".. mixture[1],
					"porcelain:slab_porcelain_" .. mixture[1])
			minetest.register_alias("stairs:stair_porcelain_".. mixture[1],
					"porcelain:stair_porcelain_" .. mixture[1])
		end

	-- stairs redo
	elseif stairs_mod and stairs.mod then
		stairs.register_all("porcelain_" .. mixture[1], "porcelain:" .. mixture[1],
			{cracky = 3},
			{"porcelain_" .. mixture[1] .. ".png"},
			mixture[2] .. " " .. S("porcelain"),
			default.node_sound_stone_defaults())

	-- default stairs
	elseif stairs_mod then
		stairs.register_stair_and_slab("porcelain_".. mixture[1], "porcelain:".. mixture[1],
			{cracky = 3},
			{"porcelain_" .. mixture[1] .. ".png"},
			mixture[2] .. " " .. S("porcelain Stair"),
			mixture[2] .. " " .. S("porcelain Slab"),
			default.node_sound_stone_defaults())
		

	end

		-- register procelain stairs and slabs recipes
		minetest.register_craft({
			type = "cooking",
			output = "stairs:slab_porcelain_" .. mixture[1],
			recipe = "stairs:slab_cold_mixture_" .. mixture[1]
		})

		minetest.register_craft({
			type = "cooking",
			output = "stairs:stair_porcelain_" .. mixture[1],
			recipe = "stairs:stair_cold_mixture_" .. mixture[1]
		})

		minetest.register_craft({
			type = "cooking",
			output = "stairs:stair_inner_porcelain_" .. mixture[1],
			recipe = "stairs:stair_inner_cold_mixture_" .. mixture[1]
		})

		minetest.register_craft({
			type = "cooking",
			output = "stairs:stair_outer_porcelain_" .. mixture[1],
			recipe = "stairs:stair_outer_cold_mixture_" .. mixture[1]
		})


	-- register porcelain for use in technic_cnc mod after all mods loaded
	if techcnc_mod then
		minetest.register_on_mods_loaded(function()
			technic_cnc.register_all("porcelain:" .. mixture[1],
				{cracky = 3, not_in_creative_inventory = 1},
				{"porcelain_" .. mixture[1] .. ".png"},
				mixture[2] .. " porcelain")
		end)
	end

	-- Cold Mixture
	-- stairs plus

	if stairsplus_mod then
		stairsplus:register_all("porcelain", "cold_mixture_" .. mixture[1],
				"porcelain:cold_mixture_" .. mixture[1], {
			description = mixture[2] .. " " .. S("cold mixture"),
			tiles = {"cold_mixture_" .. mixture[1] .. ".png"},
			groups = {cracky = 3},
			sounds = default.node_sound_stone_defaults()
		})

		if stairsplus_compat then
			stairsplus:register_alias_all("cold_mixture_", mixture[1],
					"cold_mixture_", "cold_mixture_" .. mixture[1])
			minetest.register_alias("stairs:slab_cold_mixture_".. mixture[1],
					"cold_mixture_:slab_cold_mixture_" .. mixture[1])
			minetest.register_alias("stairs:stair_cold_mixture_".. mixture[1],
					"cold_mixture_:stair_cold_mixture_" .. mixture[1])
		end

	-- stairs redo
	elseif stairs_mod and stairs.mod then
		stairs.register_all("cold_mixture_" .. mixture[1], "porcelain:cold_mixture_" .. mixture[1],
			{cracky = 3},
			{"cold_mixture_" .. mixture[1] .. ".png"},
			mixture[2] .. " " .. S("cold mixture"),
			default.node_sound_stone_defaults())

	-- default stairs
	elseif stairs_mod then
		stairs.register_stair_and_slab("cold_mixture_".. mixture[1], "porcelain:cold_mixture_".. mixture[1],
			{cracky = 3},
			{"cold_mixture_" .. mixture[1] .. ".png"},
			mixture[2] .. " " .. S("cold mixture Stair"),
			mixture[2] .. " " .. S("cold mixture Slab"),
			default.node_sound_stone_defaults())
	end

	-- register porcelain for use in technic_cnc mod after all mods loaded
	if techcnc_mod then
		minetest.register_on_mods_loaded(function()
			technic_cnc.register_all("porcelain:cold_mixture_" .. mixture[1],
				{cracky = 3, not_in_creative_inventory = 1},
				{"cold_mixture_" .. mixture[1] .. ".png"},
				mixture[2] .. " cold mixture")
		end)
	end
end






	if farming_mod then

	
		minetest.register_craftitem("porcelain:baking_soda", {
			description = S("Baking Soda"),
			inventory_image = "baking_soda.png",
			groups = {food_cornstarch = 1, food_gelatin = 1, flammable = 2, compostability = 65}
		})
		
		minetest.register_craftitem("porcelain:bottle_water", {
			description = S("Bottled Water"),
			inventory_image = "bottle_water.png",
			groups = {vessel = 1, dig_immediate = 3, attached_node = 1, drink = 0.2, handy = 1},
			is_ground_content = false,
			on_use = minetest.item_eat(2, "vessels:glass_bottle"),
			sounds = farming.node_sound_glass_defaults()
		})
	
	-- register cold mix recipe
		minetest.register_craft({
			output = "porcelain:cold_mixture_natural 9",
			replacements = {{"farming:cornstarch","farming:bowl"},{"porcelain:bottle_water","vessels:glass_bottle"},{"porcelain:baking_soda","farming:bowl"}},
			recipe = {
				{"farming:cornstarch", "porcelain:bottle_water", "porcelain:baking_soda"},
				{"", "", ""},
				{"", "", ""}
			}
		})
		
		minetest.register_craft({
			output = "porcelain:baking_soda 4",
			replacements = {{"farming:salt","vessels:glass_bottle"},{"porcelain:bottle_water","vessels:glass_bottle"}},
			recipe = {
				{"", "", ""},
				{"porcelain:bottle_water", "ethereal:orange", "farming:salt"},
				{"", "farming:bowl", ""}
			},
		})
	
		minetest.register_craft({
			output = "porcelain:bottle_water 6",
			recipe = {
				{"", "default:water_source", ""},
				{"vessels:glass_bottle", "vessels:glass_bottle", "vessels:glass_bottle"},
				{"vessels:glass_bottle", "vessels:glass_bottle", "vessels:glass_bottle"}
			}
		})
	

	else

	-- register mixture craft recipe
	minetest.register_craft({
		output = "porcelain:cold_mixture_natural 2",
		recipe = {
			{"", "", ""},
			{"default:snowblock", "default:water_source", "default:water_source"},
			{"", "", ""}
		}
	})

end









-- register a few extra dye colour options

minetest.register_craft( {
	type = "shapeless",
	output = "dye:green 4",
	recipe = {"default:cactus"}
})

minetest.register_craft( {
	type = "shapeless",
	output = "dye:brown 4",
	recipe = {"default:dry_shrub"}
})

-- only add light grey recipe if unifieddye mod isnt present (conflict)

if not minetest.get_modpath("unifieddyes") then

	minetest.register_craft( {
		type = "shapeless",
		output = "dye:dark_grey 3",
		recipe = {"dye:black", "dye:black", "dye:white"}
	})

	minetest.register_craft( {
		type = "shapeless",
		output = "dye:grey 3",
		recipe = {"dye:black", "dye:white", "dye:white"}
	})
end





-- get mod path
local path = minetest.get_modpath("porcelain")
print ("[MOD] procelain loaded")
