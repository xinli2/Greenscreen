###
### Author: Xin L
### Description: In thIs PA, you'll be writing a program that can
### combine a still image with a green, blue or red screen, with
### background(or fill) image. You should call your python file
### greenscreen.py

def get_image_dimensions_string(file_name):
    '''
    Given the file name for a valid PPM file, this function will return the
    image dimensions as a string. For example, if the image stored in the
    file is 150 pixels wide and 100 pixels tall, this function should return
    the string '150 100'.
    file_name: A string. A PPM file name.
    '''
    image_file = open(file_name, 'r')
    image_file.readline()
    return image_file.readline().strip('\n')

def new_image_algorithm(channel, image_a, image_b, cd):
    list_final = []
    i = 0
    for row in image_a:
        index = 0
        row_lst = []
        for column in row:
            if channel == 'g':
                if (int(column[0]) * cd < column[1]) and (int(column[2]) * cd < column[1]):
                    row_lst.append(image_b[i][index])
                else:
                    row_lst.append(column)
            elif channel == 'r':
                if (int(column[1]) * cd < column[0]) and (int(column[2]) * cd < column[0]):
                    row_lst.append(image_b[i][index])
                else:
                    row_lst.append(column)
            elif channel == 'b':
                if (int(column[0]) * cd < column[2]) and (int(column[1]) * cd < column[2]):
                    row_lst.append(image_b[i][index])
                else:
                    row_lst.append(column)
            index += 1
        list_final.append(row_lst)
        i += 1
    return list_final



def load_image_pixels(file_name):
    ''' Load the pixels from the image saved in the file named file_name.
    The pixels will be stored in a 3d list, and the 3d list will be returned.
    Each list in the outer-most list are the rows of pixels.
    Each list within each row represents and individual pixel.
    Each pixels is representd by a list of three ints, which are the RGB values of that pixel.
    '''
    pixels = []
    image_file = open(file_name, 'r')

    image_file.readline()
    image_file.readline()
    image_file.readline()

    width_height = get_image_dimensions_string(file_name)
    width_height = width_height.split(' ')
    width = int(width_height[0])
    height = int(width_height[1])

    for line in image_file:
        line = line.strip('\n ')
        rgb_row = line.split(' ')
        row = []
        for i in range(0, len(rgb_row), 3):
            pixel = [int(rgb_row[i]), int(rgb_row[i+1]), int(rgb_row[i+2])]
            row.append(pixel)
        pixels.append(row)

    return pixels


def write_new_image(pixels, read_file, write_file):
    file = open(read_file,'r')
    line = file.readline()
    line_w_h = file.readline()
    line_max = file.readline()
    file_write = open(write_file,'w')
    file_write.write(line)
    file_write.write(line_w_h)
    file_write.write(line_max)
    colors = ''
    for row in pixels:
        for pixel in row:
            colors += str(pixel[0])+' '+str(pixel[1])+' '+str(pixel[2])+' '
        colors += '\n'
    file_write.write(colors)


def main():
    channel = input('Enter color channel\n')
    # Get the 5 input values from the user, as described in the PA specification
    # These input values will be validated later in main
    # Next, Do some valiation of the input values
    # The PA specification tells you what you need to validate

    # If the the input is valid, implement the greenscreen.
    # You should:
    #    * Load in the image data from the two input image files.
    #      Use the provided load_image_pixels functions for this!
    #    * Generate a NEW image based on the two input values,
    #      using the greenscreen algorithm described in the specification
    #    * Save the newly-generated image to a file
    # You probably will want to create other function(s) that you call from here.
    if channel == 'r' or channel == 'b' or channel == 'g':
        channel_difference = float(input('Enter color channel difference\n'))
        if channel_difference >= 1.0 and channel_difference <= 10.0:
            gs_file = input('Enter greenscreen image file name\n')

            fi_file = input('Enter fill image file name\n')

            if get_image_dimensions_string(gs_file) == get_image_dimensions_string(fi_file):
                out_file = input('Enter output file name\n')

                image_a = load_image_pixels(gs_file)
                image_b = load_image_pixels(fi_file)
                pixels = new_image_algorithm(channel, image_a, image_b, channel_difference)
                write_new_image(pixels, gs_file, out_file)
                print('Output file written. Exiting.')
            else:
                print('Images not the same size. Will exit.')
        else:
            print('Invalid channel difference. Will exit.')
    else:
        print('Channel must be r, g, or b. Will exit.')

main()
