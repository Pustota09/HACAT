import telebot
from telebot import types
import openpyxl

from pixellib.instance import instance_segmentation

bot = telebot.TeleBot('1157810407:AAHwvYtta12trNgT2hXUq9HtzdAuYU05JzI');

@bot.message_handler(commands=['start'])
def start(message):
	markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
	b1 = types.KeyboardButton("РћС‚РїСЂР°РІРёС‚СЊ С„РѕС‚Рѕ РЅР° РїСЂРѕРІРµСЂРєСѓ")
	markup.add(b1)
	bot.send_message(message.chat.id, text = 'РџСЂРёРІРµС‚', reply_markup=markup)

@bot.message_handler(content_types=['text'])
def message(message):

	if message.text == "РћС‚РїСЂР°РІРёС‚СЊ С„РѕС‚Рѕ РЅР° РїСЂРѕРІРµСЂРєСѓ":
		bot.send_message(message.from_user.id, "РҐРѕСЂРѕС€Рѕ Р¶РґСѓ") 

@bot.message_handler(content_types=['photo'])
def handle_photo(message):
	photo = message.photo[-1]
	file_info = bot.get_file(photo.file_id)
	downloaded_file = bot.download_file(file_info.file_path)
	save_path = 'photoL.bmp'
	with open(save_path, 'wb') as new_file:
		new_file.write(downloaded_file)
	bot.send_message(message.from_user.id, "РРґС‘С‚ РѕР±СЂР°Р±РѕС‚РєР°") 
	def object1():
		sagment_image = instance_segmentation()
		sagment_image.load_model("mask_rcnn_coco17.h5")

		sagment_image.segmentImage(
				image_path="photoL.bmp",
				output_image_name="oopr.jpg"
			)


	object1()
	bot.send_photo(message.from_user.id, open("oopr.jpg", 'rb'))


bot.polling()














'''
#--------------------------------
def skaner():

	def object1():
		sagment_image = instance_segmentation()
		sagment_image.load_model("D:\\mask_rcnn_coco17.h5")

		sagment_image.segmentImage(
				image_path="testrr5.bmp",
				output_image_name="oopr.jpg"

			)


	def main():
		object1()

if __name__ == "__main__":
	main()

'''
